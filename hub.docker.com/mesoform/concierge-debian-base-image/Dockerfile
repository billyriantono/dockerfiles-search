FROM debian:jessie
LABEL maintainer="dan <dan@mesoform.com>"
LABEL description="Mesoform base Debian Jessie image which uses the autopilot pattern for self-orchestration"
LABEL com.mesoform.baseimage="True"
LABEL com.joyent.autopilotpattern="True"
LABEL com.mesoform.builddate="2019-06-16T08:57:10Z"
LABEL com.mesoform.baseimage.ver="debian:jessie"
LABEL com.docker.img.ver="mesoform/concierge-debian-base-image:0.1.32"


#################################
### General environment setup ###

# set Dockerfile build-time arguments
ARG APT_FLAGS_COMMON="-qq -y"
ARG APT_FLAGS_PERSISTANT="${APT_FLAGS_COMMON} --no-install-recommends"
ARG APT_FLAGS_DEV="${APT_FLAGS_COMMON} --no-install-recommends"
ARG ZABBIX_SOURCES=svn://svn.zabbix.com/tags/4.2.0/
ARG ZABBIX_SHORT_VERSION=4.2

# set container environment variables
ENV TERM=xterm
ENV CONTAINERPILOT_VERSION 3.8.0
ENV CONTAINERPILOT /etc/containerpilot.json5
ENV ZABBIX_VERSION=4.2.0
ENV LOG_FORMAT=text
ENV LOG_LEVEL=INFO
ENV BASE_IMG=debian:jessie
ENV FOUNDATION_IMG="mesoform/concierge-debian-base-image:0.1.32"
ENV HOSTMETADATA=concierge-debian-base-image.dockerlx
ENV CONSUL_AGENT=TRUE
ENV CONSUL_VERSION=1.5.1
ENV CONSUL_TEMPLATE_VERSION=0.20.0
ENV CONCIERGE_COURIER_URL=https://raw.githubusercontent.com/mesoform/concierge_courier/master/src/concierge_courier/concierge_courier.py
ENV CONCIERGE_COURIER_LOC=/usr/local/bin/concierge_courier.py
ENV PIS_FILE=https://raw.githubusercontent.com/mesoform/Container-Platform-Scripts/master/src/platform_integration/platform_integration.sh
ENV PIS_LOC=/usr/local/bin/platform_integration.sh


# Install some basic operating utilities
RUN apt-get ${APT_FLAGS_COMMON} update && \
    apt-get ${APT_FLAGS_PERSISTANT} install \
            ca-certificates \
            supervisor \
            curl \
            wget \
            unzip \
            python-requests \
            libssl1.0.0  && \
    rm -rf /var/cache/apt/*


##############################
### Install ContainerPilot ###

RUN curl -Lso /tmp/containerpilot.tar.gz \
    "https://github.com/joyent/containerpilot/releases/download/${CONTAINERPILOT_VERSION}/containerpilot-${CONTAINERPILOT_VERSION}.tar.gz" && \
    echo "$(curl -Ls "https://github.com/joyent/containerpilot/releases/download/${CONTAINERPILOT_VERSION}/containerpilot-${CONTAINERPILOT_VERSION}.sha1.txt" | awk '{print $1}')  /tmp/containerpilot.tar.gz" | sha1sum -c && \
    tar zxf /tmp/containerpilot.tar.gz -C /usr/local/bin && \
    rm /tmp/containerpilot.tar.gz

######################
### Install Consul ###
# Releases at https://releases.hashicorp.com/consul

RUN export archive=consul_${CONSUL_VERSION}_linux_amd64.zip && \
    curl -Lso /tmp/${archive} https://releases.hashicorp.com/consul/${CONSUL_VERSION}/${archive} && \
    echo "$(curl -Ls "https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_SHA256SUMS" | grep ${archive} | awk '{print $1}')  /tmp/${archive}" | sha256sum -c && \
    cd /usr/local/bin && \
    unzip /tmp/${archive} && \
    chmod +x /usr/local/bin/consul && \
    rm /tmp/${archive}

# Create empty directories for Consul config and data
RUN mkdir -p /etc/coprocesses/consul && \
    mkdir -p /var/lib/consul


###############################
### Install Consul template ###
# Releases at https://releases.hashicorp.com/consul-template/

RUN export archive=consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip && \
    curl -Lso /tmp/${archive} \
    "https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/${archive}" && \
    echo "$(curl -Ls https://releases.hashicorp.com/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_SHA256SUMS | grep ${archive} | awk '{print $1}')  /tmp/${archive}" | sha256sum -c && \
    unzip /tmp/${archive} -d /usr/local/bin && \
    rm /tmp/${archive}


############################
### Install Zabbix Agent ###
# https://hub.docker.com/r/zabbix/zabbix-agent/~/dockerfile/

RUN addgroup --system --quiet zabbix && \
    adduser --quiet \
            --system --disabled-login \
            --ingroup zabbix \
            --home /var/lib/zabbix/ \
        zabbix && \
    mkdir -p /etc/zabbix && \
    mkdir -p /etc/coprocesses/zabbix/zabbix_agentd.d && \
    mkdir -p /var/lib/zabbix/enc && \
    mkdir -p /var/lib/zabbix/modules && \
    chown --quiet -R zabbix:root /var/lib/zabbix && \
    chown --quiet -R zabbix:root /etc/zabbix && \
    apt-get ${APT_FLAGS_COMMON} update && \
    apt-get ${APT_FLAGS_PERSISTANT} install \
            supervisor \
            libpcre3 \
            libssl1.0.0 1>/dev/null && \
    apt-get ${APT_FLAGS_COMMON} autoremove && \
    apt-get ${APT_FLAGS_COMMON} clean && \
    rm -rf /var/lib/apt/lists/*

# For now, just add Zabbix Sender from the Zabbix package
RUN wget "https://repo.zabbix.com/zabbix/${ZABBIX_SHORT_VERSION}/debian/pool/main/z/zabbix-release/zabbix-release_${ZABBIX_SHORT_VERSION}-1+jessie_all.deb" && \
    dpkg -i zabbix-release_${ZABBIX_SHORT_VERSION}-1+jessie_all.deb && \
    apt-get ${APT_FLAGS_COMMON} update && \
    apt-get ${APT_FLAGS_DEV} install \
            gcc \
            make \
            automake \
            libc6-dev \
            pkg-config \
            libssl-dev \
            libldap2-dev \
            libpcre3-dev \
            zabbix-sender \
            subversion 1>/dev/null

RUN cd /tmp/ && \
    svn --quiet export ${ZABBIX_SOURCES} zabbix-${ZABBIX_VERSION} && \
    cd /tmp/zabbix-${ZABBIX_VERSION} && \
    zabbix_revision=$(svn info ${ZABBIX_SOURCES} | grep "Last Changed Rev"|awk '{print $4;}') && \
    sed -i "s/{ZABBIX_REVISION}/$zabbix_revision/g" include/version.h && \
    ./bootstrap.sh 1>/dev/null && \
    export CFLAGS="-fPIC -pie -Wl,-z,relro -Wl,-z,now" && \
    ./configure \
            --datadir=/usr/lib \
            --libdir=/usr/lib/zabbix \
            --prefix=/usr \
            --sysconfdir=/etc/zabbix \
            --prefix=/usr \
            --enable-agent \
            --with-ldap \
            --with-openssl \
            --enable-ipv6 \
            --silent && \
    make -j"$(nproc)" -s

RUN cp /tmp/zabbix-${ZABBIX_VERSION}/src/zabbix_agent/zabbix_agentd /usr/sbin/zabbix_agentd && \
    cp /tmp/zabbix-${ZABBIX_VERSION}/src/zabbix_get/zabbix_get /usr/bin/zabbix_get && \
    cp /tmp/zabbix-${ZABBIX_VERSION}/src/zabbix_sender/zabbix_sender /usr/bin/zabbix_sender && \
    cp /tmp/zabbix-${ZABBIX_VERSION}/conf/zabbix_agentd.conf /etc/zabbix/zabbix_agentd.conf && \
    rm -rf /tmp/zabbix-${ZABBIX_VERSION}/ && \
    apt-get ${APT_FLAGS_COMMON} purge \
            gcc \
            make \
            automake \
            libc6-dev \
            pkg-config \
            libssl-dev \
            libpcre3-dev 1>/dev/null && \
    apt-get ${APT_FLAGS_COMMON} autoremove && \
    apt-get ${APT_FLAGS_COMMON} clean && \
    rm -rf /var/lib/apt/lists/*


#############################
## Fetch Concierge Courier ##
RUN curl --retry 7 --fail -Lso ${CONCIERGE_COURIER_LOC} ${CONCIERGE_COURIER_URL} && \
    chmod u+x ${CONCIERGE_COURIER_LOC}

######################################
## Fetch Platform Integration Setup ##
RUN curl --retry 7 --fail -Lso ${PIS_LOC} ${PIS_FILE} && \
    chmod u+x ${PIS_LOC}


# copy some files so that the base image can be tested
COPY metrics.json /tmp/
COPY etc /etc/
COPY bin /usr/local/bin/
RUN chmod -R +x /usr/local/bin/

# open zabbix port
EXPOSE 10050/TCP

# This may conflict with main application when agent is setup as a coprocess
#WORKDIR /var/lib/zabbix

VOLUME ["/etc/coprocesses/zabbix//zabbix_agentd.d", "/var/lib/zabbix/enc", "/var/lib/zabbix/modules"]

ENTRYPOINT ["/usr/local/bin/containerpilot"]
#ENTRYPOINT ["/bin/sh"]

#CMD ${APP_CMD:-/bin/bash}
ONBUILD RUN apt-get update && apt-get -qq -y --no-install-recommends upgrade
ONBUILD COPY etc /etc/
ONBUILD COPY bin /usr/local/bin/