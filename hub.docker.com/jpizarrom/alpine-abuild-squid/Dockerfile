FROM andyshinn/alpine-abuild:v2

RUN sudo apk update &&\
    sudo apk add --no-cache openssl-dev perl-dev autoconf automake heimdal-dev libtool libcap-dev linux-headers

COPY . /home/builder/package/

RUN sudo chown -R builder:abuild /home/builder/package

RUN /bin/abuilder -r
