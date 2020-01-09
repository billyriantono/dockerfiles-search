FROM node:latest

# Install pip3
RUN apt-get update && \
    apt-get install -y \
        python3 \
        python3-pip \
        python3-setuptools \
        groff \
        less \
    && pip3 install --upgrade pip \
    && apt-get clean

# Install awscli
RUN pip3 --no-cache-dir install --upgrade awscli
