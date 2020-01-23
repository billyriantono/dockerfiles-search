FROM        openjdk:11-jre-slim
MAINTAINER  MaM8 Martin@Macht.me
RUN         apt update && apt install wget -y &&  \
                wget -O /tmp/searchcode-server-community.tar.gz https://searchcodeserver.com/searchcode-server-community.tar.gz && \
                cd /tmp && tar zxvf /tmp/searchcode-server-community.tar.gz && \
                rm -rf /srv && mv searchcode-server-community/release /srv && \
                rm -f /tmp/searchcode-server-community.tar.gz

WORKDIR     /srv
CMD         ["sh", "searchcode-server.sh"]
EXPOSE      8080/tcp