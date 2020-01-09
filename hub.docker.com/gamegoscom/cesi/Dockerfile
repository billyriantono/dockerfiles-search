FROM python:3.7.2

LABEL maintainer="Fatih Sarhan <f9n@protonmail.com>"

ENV CESI_VERSION 2.6.7
ENV SETUP_PATH /opt/cesi
ENV CESI_CONFIG_PATH /etc/cesi.conf.toml

WORKDIR $SETUP_PATH
RUN wget --quiet --output-document cesi.tar.gz https://github.com/gamegos/cesi/releases/download/v${CESI_VERSION}/cesi-extended.tar.gz \
  && tar -xzf cesi.tar.gz \
  && rm cesi.tar.gz

WORKDIR $SETUP_PATH
RUN pip3 install -r requirements.txt
RUN pip3 install gunicorn

RUN cp defaults/cesi.conf.toml $CESI_CONFIG_PATH

WORKDIR ${SETUP_PATH}/cesi

EXPOSE 5000
ENTRYPOINT [ "gunicorn", "-b", "0.0.0.0:5000", "--log-level", "info", "--reload", "wsgi:app" ]

