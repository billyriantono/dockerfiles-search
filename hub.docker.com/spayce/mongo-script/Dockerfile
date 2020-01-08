FROM mongo:4.0.4-xenial
#FROM ubuntu:16.04

RUN apt-get update
RUN apt-get install locales

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get install -y python3-pip python3-dev \
&& cd /usr/local/bin \
&& ln -s /usr/bin/python3 python \
&& pip3 install --upgrade pip

#Dependencias
RUN pip install Flask

RUN cd /home \
&& mkdir -p /app
COPY . /app
WORKDIR /app

EXPOSE 8081

COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod 777 /usr/local/bin/docker-entrypoint.sh \
    && ln -s /usr/local/bin/docker-entrypoint.sh /
ENTRYPOINT ["docker-entrypoint.sh"]
