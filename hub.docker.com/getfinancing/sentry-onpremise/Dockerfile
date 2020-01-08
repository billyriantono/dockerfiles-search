FROM sentry:9.0-onbuild

RUN apt-get update --yes &&\
    apt-get install --yes libmysqlclient-dev &&\
    pip install mysql-python sentry-telegram


