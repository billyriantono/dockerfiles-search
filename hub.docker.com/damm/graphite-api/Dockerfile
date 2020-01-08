FROM stackbrew/ubuntu:12.04
VOLUME /srv/graphite
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list
RUN apt-get update
RUN apt-get upgrade -y

RUN apt-get install -y language-pack-en
ENV LANGUAGE en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN locale-gen en_US.UTF-8
RUN dpkg-reconfigure locales

RUN apt-get install -y libxml2-dev curl python build-essential make gcc python-dev wget git-core libffi-dev libcairo2-dev
RUN wget http://python-distribute.org/distribute_setup.py
RUN python distribute_setup.py

RUN wget https://raw.github.com/pypa/pip/master/contrib/get-pip.py
RUN python get-pip.py

RUN pip install gunicorn graphite-api[sentry,cyanite]
ONBUILD ADD graphite-api.yaml /etc/graphite-api.yaml
ONBUILD RUN chmod 0644 /etc/graphite-api.yaml

### Expose port 8080 for Gunicorn

EXPOSE 8080


CMD cd /var/tmp/graphite-api;gunicorn -w2 graphite_api.app:app -b 0.0.0.0:8080
