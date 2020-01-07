FROM avkosme/python3.6.6

ADD assets/celery.service.sh /opt/celery.service.sh
RUN chmod +x /opt/celery.service.sh
RUN /opt/celery.service.sh

ADD assets/start.sh /opt/start.sh
RUN chmod +x /opt/start.sh

ADD assets/pre.sh /opt/pre.sh
RUN chmod +x /opt/pre.sh

ADD requirements.txt /opt/requirements.txt
RUN pip3.6 install -r /opt/requirements.txt

RUN systemctl enable celery.service

COPY docker-entrypoint.sh /usr/local/bin/

RUN /bin/bash -c 'chmod +x /usr/local/bin/docker-entrypoint.sh'

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD ["sh", "-c", "/opt/init.sh"]
