FROM python:2.7.16-stretch

RUN apt-get -y update
RUN apt-get -y install \
  git \
  wget \
  sudo \
  net-tools \
  build-essential \
  libssl-dev \
  libffi-dev \
  pkg-config \
  libssl-dev \
  libffi-dev \
  libxml2-dev \
  libxslt1-dev \
  libfreetype6-dev \
  libpng-dev \
  postgresql

RUN mkdir /opt/faraday
WORKDIR /opt/faraday
RUN git init && git remote add -t \* -f origin https://github.com/infobyte/faraday.git && git pull origin master
COPY ./preflight.sh /opt/faraday
RUN chmod +x /opt/faraday/preflight.sh
WORKDIR /opt/faraday
RUN ./preflight.sh
COPY ./entrypoint.sh /root/entrypoint.sh
RUN chmod +x /root/entrypoint.sh

EXPOSE 5985

ENTRYPOINT [ "/root/entrypoint.sh" ]
