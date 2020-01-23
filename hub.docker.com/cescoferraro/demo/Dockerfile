FROM ubuntu:14.04

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive \
    apt-get install -y -q git \
    make build-essential libssl-dev zlib1g-dev libbz2-dev libreadline-dev \
    libsqlite3-dev wget curl llvm libncurses5-dev vim supervisor

RUN curl -L https://raw.githubusercontent.com/yyuu/pyenv-installer/master/bin/pyenv-installer | bash
ENV HOME  /root
ENV PYENV_ROOT $HOME/.pyenv
ENV PATH $PYENV_ROOT/shims:$PYENV_ROOT/bin:$PATH
RUN pyenv install 2.7.11
RUN pyenv global 2.7.11




#POSTGRES
RUN apt-get -y install libpq-dev


#PILLOW
RUN apt-get -y build-dep python-imaging
RUN apt-get -y install libjpeg8 libjpeg62-dev libfreetype6 libfreetype6-dev


#SUPERVISOR
RUN mkdir -p /var/log/supervisord
RUN touch /var/log/supervisord/supervisord.log
COPY supervisor/supervisord.conf /etc/supervisor/supervisord.conf
COPY supervisor/conf.d/program.conf /etc/supervisor/conf.d/program.conf




#MKDIR AND CD TO THE APP DIR




# Get pip to download and install requirements:
ADD pip/ /etc/pip
WORKDIR /etc/pip/core

#The order matter here, otherwise it will download packages
#and we want to save time, durring development
RUN pip install gunicorn-19.4.5.tar.gz \
                Werkzeug-0.11.3.tar.gz \
                itsdangerous-0.24.tar.gz \
                MarkupSafe-0.23.tar.gz \
                Jinja2-2.8.tar.gz \
                coverage-4.1b1.tar.gz \
                Flask-0.10.1.tar.gz \
                Flask-Script-2.0.5.tar.gz \

                backports.ssl_match_hostname-3.5.0.1.tar.gz \
                six-1.10.0.tar.gz \
                singledispatch-3.4.0.3.tar.gz \
                certifi-2015.11.20.1.tar.gz \
                backports_abc-0.4.tar.gz \
                tornado-4.3.tar.gz \
                livereload-2.4.0.tar.gz \

                requests-2.9.1.tar.gz \
                Flask-Testing-0.4.2.tar.gz


WORKDIR /etc/pip/extension
RUN pip install SQLAlchemy-1.0.11.tar.gz \
                Flask-SQLAlchemy-2.1.tar.gz \
                psycopg2-2.6.1.tar.gz




#COPY APP FILES (OPTIONAL)
RUN mkdir -p /srv/app
ADD webapp/ /srv/app/
WORKDIR /srv/app



CMD ["supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]




