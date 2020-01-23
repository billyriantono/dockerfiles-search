FROM telegraf:1.12.3

RUN apt-get update && \
    apt-get install -yq \
      ipmitool \
      smartmontools && \
    apt-get clean && \
    rm -rf \
	    /tmp/* \
	    /var/lib/apt/lists/* \
	    /var/tmp/*
