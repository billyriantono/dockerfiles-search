FROM alpine:3.7

ARG PYANG_VERSION=1.7.8
ENV PYANG_VERSION=${PYANG_VERSION}

WORKDIR /usr/src/

# Install Python3 and PIP
RUN apk add --no-cache \
    python3 python3-dev && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    rm -r /root/.cache

# Dependencies as an environment variable
ENV DEPS linux-headers \
    gcc \
    git \
    musl-dev \
    bash \ 
    libxslt-dev \
    libxml2-dev \
    libxslt \
    curl \
    openssh-client \
    pkgconf

# Install system dependencies (latest list of available packages)
RUN apk --update add --no-cache $DEPS

# Install pyang  
RUN wget -c https://github.com/mbj4668/pyang/archive/pyang-${PYANG_VERSION}.tar.gz -O - | tar -xz 

WORKDIR /usr/src/pyang-pyang-${PYANG_VERSION}

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Install pyang
RUN python setup.py install

WORKDIR /usr/src