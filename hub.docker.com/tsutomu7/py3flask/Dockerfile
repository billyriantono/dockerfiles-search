FROM alpine:3.4

ENV USER=scientist HOME=/home/scientist LANG=C.UTF-8
RUN export uid=1000 gid=1000 pswd=scientist && \
    apk add --no-cache musl python3 sudo redis && \
    apk add --no-cache --virtual=tzdata_pkg tzdata && \
    cp /usr/share/zoneinfo/Japan /etc/localtime && \
    apk del tzdata_pkg && \
    addgroup -g $gid $USER && \
    adduser -G $USER -S -s /bin/ash $USER && \
    mkdir -p $HOME/.cache && \
    echo "$USER:$pswd" | chpasswd && \
    echo "$USER ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/$USER && \
    chmod 0440 /etc/sudoers.d/$USER && \
    pip3 install --no-cache-dir -U pip && \
    pip install --no-cache-dir flask pyjade pyyaml markdown redis gunicorn && \
    rm -rf /root/.[ac]* $HOME/.[ac]*
USER $USER
WORKDIR $HOME
CMD ["/bin/ash"]
