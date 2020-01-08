FROM ubuntu:16.04

MAINTAINER Dockerfiles

RUN apt-get update && \
    apt-get upgrade -y && \ 
    apt-get install -y \
	git \
	python3 \
	python3-dev \
	python3-setuptools \
	python3-pip \
	nginx \
	supervisor && \
        pip3 install -U -i https://pypi.doubanio.com/simple/ pip setuptools && \
  	rm -rf /var/lib/apt/lists/*

RUN pip3 install -i https://pypi.doubanio.com/simple/ uwsgi



RUN echo "daemon off;" >> /etc/nginx/nginx.conf
COPY nginx-app.conf /etc/nginx/sites-available/default
COPY supervisor-app.conf /etc/supervisor/conf.d/


COPY requirements.txt /home/docker/code/vDirectory/
RUN pip3 install -i https://pypi.doubanio.com/simple/ -r /home/docker/code/vDirectory/requirements.txt


COPY . /home/docker/code/


EXPOSE 80
CMD ["supervisord", "-n"]
