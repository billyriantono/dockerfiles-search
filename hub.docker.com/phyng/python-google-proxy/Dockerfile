
FROM ubuntu:14.04
MAINTAINER phyng

RUN apt-get update && apt-get install -y \
  htop tree curl wget git \
  build-essential python-setuptools python-dev python-pip \
  libxml2-dev libxslt1-dev python-lxml \
  && apt-get -y --force-yes build-dep python-lxml \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*


RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV REQUESTS_CA_BUNDLE /etc/ssl/certs/ca-certificates.crt
ENV TERM xterm
ENV ENV_DOCKER true
ENV ENV_DEBUG false

RUN useradd --uid 1000 -ms /bin/bash ubuntu
RUN mkdir /home/ubuntu/project
WORKDIR /home/ubuntu/project

ADD ./requirements.txt /home/ubuntu/project/
RUN pip install -U pip -i http://pypi.douban.com/simple/
RUN pip install -r requirements.txt \
  -i http://pypi.douban.com/simple/ --trusted-host pypi.douban.com

ADD ./ /home/ubuntu/project/
USER ubuntu
CMD ["dumb-init", "gunicorn", "proxy.wsgi:application", "-b", "0.0.0.0:8001", "-w", "3"]
EXPOSE 8001
