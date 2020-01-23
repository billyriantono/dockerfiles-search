FROM python:3.7.2-alpine3.9
RUN apk add --no-cache --update git curl vim openssh ca-certificates python3-dev libstdc++ && \
    apk add --no-cache g++ && \
    ln -s /usr/include/locale.h /usr/include/xlocale.h && \
    pip3 install numpy && \
    pip3 install pandas
