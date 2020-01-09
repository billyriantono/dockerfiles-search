FROM debian:latest

RUN apt-get update && apt-get install -y wget ca-certificates gnupg && apt-get -y clean && \
  wget -q http://repositories.sensuapp.org/apt/pubkey.gpg -O- | apt-key add - && \
  echo "deb     http://repositories.sensuapp.org/apt sensu main" | tee /etc/apt/sources.list.d/sensu.list

RUN apt-get update && \
    apt-get install -y sensu procps sysstat && \
    apt-get -y clean 

ENV HOST_DEV_DIR="/host_dev" \
    HOST_PROC_DIR="/host_proc" \
    HOST_SYS_DIR="/host_sys"

ENV PATH="/opt/sensu/embedded/bin:${PATH}"

# install plugins
RUN gem install sensu-plugins-cpu-checks && \
    gem install sensu-plugins-memory-checks && \
    gem install sensu-plugins-network-checks

# use host (not container) dirs for checks and metrics
#RUN /bin/bash -c  'if compgen -G "/opt/sensu/embedded/bin/*.rb" > /dev/null; then \
#      sed -i "s|/dev|$HOST_DEV_DIR|g" /opt/sensu/embedded/bin/*.rb; \
#      sed -i "s|/proc|$HOST_PROC_DIR|g" /opt/sensu/embedded/bin/*.rb; \ 
#      sed -i "s|/sys|$HOST_SYS_DIR|g" /opt/sensu/embedded/bin/*.rb; \
#    fi'

RUN mkdir -p /etc/sensu/conf.d mkdir -p /etc/sensu/ssl
ADD ./config /etc/sensu/conf.d
ADD ./ssl /etc/sensu/ssl
WORKDIR /opt/sensu/bin

CMD ["./sensu-client", "-d" , "/etc/sensu/conf.d"]