#FROM python:3.3.6
FROM python:3.5.3

MAINTAINER yefryfigueroa122@gmail.com

RUN apt-get update && apt-get install -y \
	sqlite3 \
  supervisor \
  libmysqlclient-dev\
  vim \
  && rm -rf /var/lib/apt/lists/*

COPY config/app-supervisor.conf /etc/supervisor/conf.d/
COPY app/* /code/app/
COPY config/uwsgi.ini /code/
RUN pip install -r /code/app/requirements.txt
RUN chmod +x /code/app/docker-entrypoint.sh


RUN apt-get update && apt-get install -y wget
ENV DOCKERIZE_VERSION v0.2.0
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz


RUN cd ~
RUN curl -sL https://deb.nodesource.com/setup_6.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh
RUN apt-get install nodejs
WORKDIR /code/app/
RUN npm install -g 
RUN npm install -g webpack
RUN npm install
#RUN pip install wagtail==1.13.1


EXPOSE 3031

#CMD ["supervisord", "-n"]
