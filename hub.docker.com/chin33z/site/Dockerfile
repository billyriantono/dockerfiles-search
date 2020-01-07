FROM debian:stable

RUN \
  apt-get update && \
  apt-get install -y git vim-nox \
                    screen wget xz-utils unzip python-pip python-dev nginx python-virtualenv &&\
  rm -rf /var/lib/apt/lists/* &&\
  apt-get clean -yq


RUN cd ~ &&\
    git clone https://github.com/chin33z/microblog.git

RUN cd ~/microblog &&\
    virtualenv flask &&\
    flask/bin/pip install flask flask-login flask-openid flask-mail flask-sqlalchemy sqlalchemy-migrate flask-whooshalchemy flask-wtf \
    flask-babel guess_language flipflop coverage &&\
    flask/bin/python db_create.py &&\
    flask/bin/python db_upgrade.py


ENV HOME /root
WORKDIR /root
