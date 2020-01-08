FROM fedora:21

MAINTAINER Andre Vehreschild
# yum clean all && \

RUN yum -y update && yum -y install sudo calligra xlogo && \
    export uid=1000 gid=1000 && \
    mkdir -p /home/caluser && \
    echo "caluser:x:${uid}:${gid}:Calligra User,,,:/home/caluser:/bin/bash" >> /etc/passwd && \
    echo "caluser:x:${uid}:" >> /etc/group && \
    echo "caluser ALL=(ALL) NOPASSWD: ALL" >/etc/sudoers.d/caluser && \
    chmod 0440 /etc/sudoers.d/caluser && \
    chown ${uid}:${gid} -R /home/caluser

USER caluser
ENV HOME /home/caluser

CMD export QT_GRAPHICSSYSTEM="native" ; /usr/bin/calligrasheets


