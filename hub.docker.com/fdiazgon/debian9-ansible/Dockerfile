FROM debian:stretch
LABEL maintainer="Fernando Díaz"

ENV DEBIAN_FRONTEND noninteractive

RUN if ! command -v gpg > /dev/null; then \
 		  apt-get update && apt-get install -y --no-install-recommends \
		  gnupg2 dirmngr \
 		  && rm -rf /var/lib/apt/lists/* \
      && rm -rf /usr/share/doc && rm -rf /usr/share/man \
      && apt-get clean; \
 	  fi

RUN echo "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main" | tee -a /etc/apt/sources.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 \
    && apt-get update && apt-get install -y --no-install-recommends \
    ansible sudo systemd curl \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /usr/share/doc && rm -rf /usr/share/man \
    && apt-get clean

RUN mkdir -p /etc/ansible \
    && echo "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts
