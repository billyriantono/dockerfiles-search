FROM anapsix/alpine-java:7_jdk

RUN apk update \
    && apk add python libsodium unzip wget iptables libcap  libcap-dev \
    && apk del  wget  unzip
    
CMD ["sh", "-c", "/start.sh"]
