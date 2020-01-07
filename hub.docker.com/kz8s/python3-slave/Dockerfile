FROM jenkinsci/ssh-slave

RUN set -eux &&\
    apt-get update &&\
    apt-get upgrade -y &&\
    apt-get install -yq python3 python3-pip vim &&\
    apt-get clean &&\
    rm -rf /var/lib/apt-lists/* &&\
    rm -f /var/cache/apt/*.bin

