FROM ubuntu:18.04
 
COPY script/entrypoint.sh /entrypoint.sh

ENV DEBIAN_FRONTEND=noninteractive \
    GSE_PASSWORD=admin \
    HOSTNAME=gs \
    SRC_DIR=gse-git \
    SRC_PATH=/root/${SRC_DIR} \
    PGUSERNAME=root


RUN apt-get update ;\
    apt-get install apt-utils software-properties-common --no-install-recommends -yq ;\
    apt-get dist-upgrade -yq ;\
    apt-get install \
        redis-server \
        sudo \
        curl \
        python-polib \
        rsync \
        vim \
        nano \
        -yq ;\
    apt-get clean -yq

CMD /entrypoint.sh
