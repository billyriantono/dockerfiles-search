FROM alpine:latest

RUN apk update --no-cache && \
    apk upgrade --no-cache && \
    apk add bash curl git make --no-cache

RUN git clone https://github.com/git-ftp/git-ftp.git /opt/git-ftp \
    && cd /opt/git-ftp \
    && make install \
    && rm -rf /opt/git-ftp

CMD ["bash"]
