FROM alpine

ENV JET_HOME=$HOME/jet

RUN mkdir ${JET_HOME}
ADD jet/ $JET_HOME
ADD docker-entrypoint.sh /
COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x ${JET_HOME} -R
RUN chmod +x docker-entrypoint.sh

EXPOSE 1027
WORKDIR $JET_HOME

ENV USER jet

CMD ["/docker-entrypoint.sh"]
