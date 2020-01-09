FROM andrius/alpine-asterisk:14

RUN curl -s https://www.kaigara.org/get | sh

COPY bin/entrypoint.sh /usr/bin/
RUN chmod 755 /usr/bin/entrypoint.sh
ENTRYPOINT ["/usr/bin/entrypoint.sh"]

COPY ./operations/ /opt/kaigara/operations/
COPY ./resources/ /etc/kaigara/resources/
COPY ./metadata/ /etc/kaigara/metadata/
