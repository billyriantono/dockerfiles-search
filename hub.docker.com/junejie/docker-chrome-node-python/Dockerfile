FROM junejie/docker-chrome-node:r2

RUN apt-get update
RUN python3 --version
RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py && pip --version
RUN pip install virtualenv
RUN apt-get install python3-dev -y
RUN apt-get install build-essential autoconf libtool pkg-config python-opengl python-imaging python-pyrex -y
