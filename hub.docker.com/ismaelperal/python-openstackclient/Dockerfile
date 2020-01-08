FROM python:3.7-slim-stretch

RUN apt-get update && apt-get install -y \
    gcc \
 && rm -rf /var/lib/apt/lists/* \
 && pip install python-openstackclient \
 && rm -rf /root/.cache 

CMD [ "openstack" ]
