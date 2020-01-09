from sonatype/nexus3

ARG root_password

COPY permission_and_start.sh /tmp

USER root

RUN echo "root:"$root_password | chpasswd

USER nexus

ENTRYPOINT ['sh']
CMD ['/tmp/permission_and_start.sh']
