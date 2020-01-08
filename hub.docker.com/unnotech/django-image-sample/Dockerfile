FROM deanunnotech/django-image-sample:latest
# FROM python:2.7

WORKDIR /usr/src/app
COPY . .
RUN pip install -r requirements.txt
RUN django-admin startproject project .; exit 0
EXPOSE 8000:8000
CMD supervisord -c supervisord.conf --nodaemon
# CMD ping google.com