FROM ibmcom/db2express-c:latest
MAINTAINER Eliezio Oliveira github@eliez.io

ENV TINI_VERSION v0.14.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

COPY entrypoint.sh /
RUN mkdir /initdb.d
ENTRYPOINT ["/tini", "/entrypoint.sh"]

VOLUME ["/home/db2inst1/db2inst1", "/home/db2inst1/sqllib/sqldbdir"]

EXPOSE 50000

CMD ["db2start"]

