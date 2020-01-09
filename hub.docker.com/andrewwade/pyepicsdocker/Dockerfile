FROM debian:jessie-slim


# set environment variables so epics base and modules know how to build
ENV EPICS_HOST_ARCH="linux-x86_64" \
    EPICS_ROOT="/opt/epics" \
    EPICS_BASE="/opt/epics/base" \
    EPICS_BASE_BIN="/opt/epics/base/bin/linux-x86_64" \
    EPICS_BASE_LIB="/opt/epics/base/lib/linux-x86_64" \
    PATH="/opt/epics/base/bin/linux-x86_64/:${PATH}"


# Build the epics base for access to channels through pyepics
RUN apt-get update -q \
    && apt-get --yes install \
       curl g++ make libperl-dev libreadline-dev wget \
       python python-pip \
    && mkdir -p /opt/epics/modules \
    && wget https://epics.anl.gov/download/base/base-3.15.5.tar.gz \
    && tar xvzf base-3.15.5.tar.gz -C /opt/epics/ \
    && rm base-3.15.5.tar.gz \
    && ln -s /opt/epics/base-3.15.5 /opt/epics/base \
    && cd /opt/epics/base \
    && make \
    && apt-get --yes purge \
       curl g++ make libperl-dev libreadline-dev wget \
    && apt-get clean

COPY requirements.txt /

RUN apt-get -y install libc-dev
RUN apt-get -y install build-essential
RUN pip install -U pip

# Install pyepics requirements
RUN pip install -r /requirements.txt

COPY . /app
WORKDIR /app

CMD ["python", "test.py"]
