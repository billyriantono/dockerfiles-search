FROM larry850806/workspace-base

# setup env for python
ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8

# install python3.6 and pip3
RUN echo "deb http://ftp.de.debian.org/debian testing main" > /etc/apt/sources.list && \
    apt-get -y update && \
    apt-get -y install python3.6 python3-pip && \
    apt-get clean

# setup link: python -> python3, pip -> pip3
RUN ln -s /usr/bin/python3.6 /usr/bin/python && \
    ln -s /usr/bin/pip3 /usr/bin/pip

# install pipenv
# RUN pip install pipenv --no-cache-dir

