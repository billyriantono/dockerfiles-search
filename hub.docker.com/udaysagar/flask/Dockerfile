FROM ubuntu:14.04

RUN apt-get update
RUN apt-get -y install python python-pip
RUN pip install flask
RUN pip install flask && \
    pip install flask-login && \
    pip install flask-openid && \
    pip install flask-mail && \
    pip install flask-sqlalchemy && \
    pip install sqlalchemy-migrate && \
    pip install flask-whooshalchemy && \
    pip install flask-wtf && \
    pip install flask-babel && \
    pip install guess_language && \
    pip install flipflop && \
    pip install coverage

ADD app /app

WORKDIR /app
CMD python app.py
