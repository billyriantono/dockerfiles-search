FROM alpine:3.8

LABEL maintainer "eric@daras.family"

# Install updates
RUN apk update

# Base packages
RUN apk add git curl python py-pip

# Clone pystemon repository
RUN mkdir /opt
RUN cd /opt && \
    git clone https://github.com/cvandeplas/pystemon && \
    cd pystemon && \
    rm -Rf .git

# Install required python packages	
RUN pip install -r /opt/pystemon/requirements.txt

# Install entrypoint
ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
RUN mv /opt/pystemon/pystemon.yaml /tmp
RUN mkdir /opt/pystemon/config

# Volumes
VOLUME /opt/pystemon/config
VOLUME /opt/pystemon/archive
VOLUME /opt/pystemon/alerts

WORKDIR /opt/pystemon

ENTRYPOINT ["/entrypoint.sh"]
