FROM debian:wheezy

MAINTAINER "Michael Wright <mkwright@gmail.com>"

# Install the core system tools
RUN apt-get update && apt-get --assume-yes --force-yes install build-essential curl tar vim 

# Install the python dependencies
#RUN apt-get install --assume-yes --force-yes python3 python3-dev python3-pip (python3.2 didn't work for me)
RUN apt-get install -y libncursesw5-dev libreadline-gplv2-dev libssl-dev libgdbm-dev \ 
      libc6-dev zlib1g-dev libbz2-dev liblzma-dev

RUN cd /tmp && \
    curl https://www.python.org/ftp/python/3.4.0/Python-3.4.0.tgz | tar xvz && \
    cd Python-3.4.0 && \
    ./configure --prefix=/usr/local/python3 && \ 
    make install && \
    cd /tmp && \
    rm -rf Python-3.4.0 

# Install pip for python3
RUN curl http://raw.github.com/pypa/pip/master/contrib/get-pip.py | /usr/local/python3/bin/python3

# Set the path for things
RUN ln -s /usr/local/python3/bin/python3 /usr/bin/python3 && \
    ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3 

