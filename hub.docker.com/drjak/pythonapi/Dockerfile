FROM ubuntu:latest
RUN apt-get update
RUN apt-get -y install python3.7 virtualenv 
ENTRYPOINT [ "/usr/bin/virtualenv -p /usr/local/lib/python3.7 /opt/dowozy/dowozy-API/env; /opt/dowozy/dowozy-API/env/bin/pip install -r /opt/dowozy/dowozy-API/api/requirements.txt; /opt/dowozy/dowozy-API/env/bin/python /opt/dowozy/dowozy-API/api/manage.py runserver 0.0.0.0:8080" ]
