FROM openjdk:8
MAINTAINER filippo@clipperz.is

RUN mkdir /perfino_installation

WORKDIR /perfino_installation

RUN wget https://download-gcdn.ej-technologies.com/perfino/perfino_unix_3_2_2.sh && \
    chmod a+x perfino_unix_3_2_2.sh && \
    ./perfino_unix_3_2_2.sh -q && \
    rm -f perfino_unix_3_2_2.sh

EXPOSE 8020 8847

VOLUME /var/opt/perfino

ENTRYPOINT /usr/local/perfino/bin/perfino_console
