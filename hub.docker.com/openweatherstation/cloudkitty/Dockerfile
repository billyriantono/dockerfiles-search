FROM docker.io/library/centos:7 AS builder

COPY .  /root/cloudkitty/
WORKDIR /root/cloudkitty/

RUN yum -y update                                               &&  \
    yum -y install                                                  \
        epel-release                                                \
        gcc                                                         \                         
        git                                                     &&  \
    # pip is in epel-release so we have to split 
    yum -y install                                                  \
        python-devel                                                \
        python-pip                                              &&  \
    pip install -r requirements.txt                             &&  \
    # we install in a prefix for multilayer
    pip install -r requirements.txt -I --prefix=/opt/cloudkitty &&  \
    python setup.py install            --prefix=/opt/cloudkitty


FROM docker.io/library/centos:7

COPY --from=builder /opt/cloudkitty/ /usr/
COPY --from=builder /root/cloudkitty/contrib/docker/etc/cloudkitty /etc/cloudkitty

EXPOSE 8889
