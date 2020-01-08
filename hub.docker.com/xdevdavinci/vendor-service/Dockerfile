FROM xdevdavinci/python3.6

RUN pip3 install --upgrade pip setuptools flake8 ipdb

ENV DJANGO_SETTINGS_MODULE vendor_service.settings.dev

RUN echo 'alias rs="python3 manage.py migrate && python3 -m vendor_service.standalone -s vendor_service.settings.dev --use-file-watcher vendor_service,pysoa,conformity"' >> ~/.bashrc

WORKDIR /srv/vendor_service

ADD . /srv/vendor_service/
RUN pip3 install -e /srv/vendor_service[testing]

COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]

CMD [ "python3", "-m", "vendor_service.standalone", "-s",  "vendor_service.settings.dev", "--use-file-watcher", "vendor_service,pysoa,conformity" ]
