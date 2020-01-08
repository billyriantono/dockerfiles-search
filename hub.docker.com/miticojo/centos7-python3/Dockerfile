FROM centos:7
MAINTAINER Giorgio Crivellari <miticojo@gmail.com>

# set python version to install
ARG PYTHON_VER=3.5.2
ENV PYTHON_URL=https://www.python.org/ftp/python/$PYTHON_VER/Python-$PYTHON_VER.tgz

# install minimum requirements to compile, run compilation, install pip and virtualenv, finally clean used files
RUN yum install -y gcc make openssl-devel\
  && curl $PYTHON_URL | tar -xzf -  -C /usr/src/ \
  && cd /usr/src/Python-$PYTHON_VER \
  && ./configure && make install \
  && curl "https://bootstrap.pypa.io/get-pip.py" | python  \
  && pip install virtualenv \
  && rm -rf /var/cache/apk/* && rm -rf /usr/src/Python-*

# Examples lines 
# WORKDIR /app

# COPY . /app
# RUN virtualenv /env && /env/bin/pip install -r /app/requirements.txt

# EXPOSE 5000
# CMD ["/env/bin/python", "app.py"]
