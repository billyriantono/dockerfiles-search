FROM alpine:latest

ENV IDEA_HOME=$HOME/idea
RUN mkdir ${IDEA_HOME}
COPY idea/ $IDEA_HOME
RUN chmod +x ${IDEA_HOME} -R

COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

EXPOSE 1027
WORKDIR $IDEA_HOME

ENV USER chenmi

CMD ["docker-entrypoint.sh"]
