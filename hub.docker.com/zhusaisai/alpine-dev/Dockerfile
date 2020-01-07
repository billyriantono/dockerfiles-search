FROM alpine:3.8
RUN apk update && apk upgrade; \
 apk --no-cache add vim \
 git \
 gcc \
 g++ \
 gdb \
 nginx \
 go \
 lua \
 bash \
 bash-completion \
 bash-doc \
 tzdata \
 clang \
 make \
 nmap \
 ctags \ 
 less \
 openssl; \
 rm -rf /var/cache/apk/* && rm -rf /var/lib/apt/lists/*
COPY config /root/config
RUN bash /root/config/config.sh;
WORKDIR /root
# VOLUME /data
CMD [ "/bin/bash" ]
