FROM debian:jessie

MAINTAINER Milo Casagrande <milo.casagrande@linaro.org>
LABEL Version="1.0" Description="Run a simple web app as website and signup process"

RUN apt-get clean && apt-get update -qq && apt-get install -qq -y --no-install-recommends \
    git \
    openssh-client \
    python3 \
    python3-dev \
    python3-pip \
    virtualenv \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

RUN cd /srv ; git clone https://github.com/linaro-product/gitci-signup.git
RUN mkdir -p /srv/gitci-signup-env

ENV PYTHONUSERBASE /srv/gitci-signup-env
RUN pip3 install -q -r /srv/gitci-signup/requirements.txt --user

COPY gitci-signup-uwsgi.ini /srv
COPY gitci-signup.cfg /srv

COPY start.sh /
RUN chmod +x /start.sh

EXPOSE 5000

CMD ["/start.sh"]
