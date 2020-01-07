FROM phusion/baseimage:latest
CMD ["/sbin/my_init"]

RUN apt-get update -y && apt-get install --no-install-recommends -y -q build-essential python2.7 python2.7-dev python-pip git
RUN pip install -U pip
RUN pip install virtualenv

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
