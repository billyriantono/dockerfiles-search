FROM i386/ubuntu:18.04

MAINTAINER fluendo

ENV DEBIAN_FRONTEND noninteractive

# Create the worker dir
RUN mkdir /worker
RUN chmod 777 /worker
WORKDIR /worker

# Install required packages
RUN apt-get update && \
    apt-get upgrade -y && \ 
    apt-get install -y \
        python2.7 \
        python2.7-dev \
        python-setuptools \
        python-pip \
        git wget subversion && \
        pip install -U pip setuptools

# Install buildbot requirements
RUN pip install buildbot-worker

# Install ldap support
RUN apt-get -y install sudo wget libnss-ldap

# Fix the uname call outputing 64 bits arch on 32 bits docker image.
ENTRYPOINT ["linux32", "--"]

COPY run.sh .
CMD ["./run.sh"]
