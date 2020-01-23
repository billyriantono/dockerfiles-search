FROM alpine
WORKDIR /opt/
RUN apk add --no-cache make gcc g++ python git libpng libcap libreoffice tar gzip build-base
RUN wget https://github.com/pocoproject/poco/archive/poco-1.7.1-release.tar.gz
RUN mkdir /opt/poco
RUN tar xzf poco-*.tar.gz -C /opt/poco
RUN ls
RUN cd /opt/poco && ls
RUN configure && 
    make &&
    make install
RUN cd /opt/ && git clone https://github.com/LibreOffice/online.git && git clone https://github.com/LibreOffice/core.git
RUN cd /opt/online/loolwsd && MASTER=/opt/core &&
    autoreconf &&
    automake --add-missing &&
    configure --enable-silent-rules --with-lokit-path=${MASTER}/include --with-poco-includes=/opt/poco/include --with-poco-libs=opt/poco/lib &&
    make
