FROM openjdk:8-jdk

COPY entrypoint /usr/local/bin/entrypoint
RUN chmod +x /usr/local/bin/entrypoint && \
    mkdir /minecraft

WORKDIR /minecraft

ENTRYPOINT ["entrypoint"]
