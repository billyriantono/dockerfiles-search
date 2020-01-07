FROM python:3.7

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y \
		gcc \
		gettext \
		mysql-client \				
	--no-install-recommends && rm -rf /var/lib/apt/lists/*

RUN pip install mysqlclient django==2.1.7
RUN django-admin startproject myapp


EXPOSE 8000

CMD python /usr/src/app/myapp/manage.py runserver 0.0.0.0:8000
