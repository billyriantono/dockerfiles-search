FROM xdevdavinci/python3.6

RUN pip3 install --upgrade pip setuptools flake8 ipdb

ENV DJANGO_SETTINGS_MODULE user_service.settings.dev

RUN echo 'alias rs="python3 manage.py migrate && python3 -m user_service.standalone -s user_service.settings.dev --use-file-watcher user_service,pysoa,conformity"' >> ~/.bashrc

WORKDIR /srv/user_service

ADD . /srv/user_service/
RUN pip3 install -e /srv/user_service[testing]

COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]

CMD [ "python3", "-m", "user_service.standalone", "-s",  "user_service.settings.dev", "--use-file-watcher", "user_service,pysoa,conformity" ]
