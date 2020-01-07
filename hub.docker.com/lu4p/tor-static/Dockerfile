FROM lu4p/xgo-custom

RUN apt-get update && apt-get upgrade -y && apt-get install -y tor build-essential libtool autopoint wget unzip
RUN mkdir -p /go/src/github.com/cretz/tor-static

#get linux libs
RUN cd /go/src/github.com/cretz/tor-static  && wget https://github.com/lu4p/tor-static/releases/download/linux/libs_linux.tar.gz

#get windows libs
RUN cd /go/src/github.com/cretz/tor-static  && wget https://github.com/lu4p/tor-static/releases/download/2/tor-static-windows-amd64.zip