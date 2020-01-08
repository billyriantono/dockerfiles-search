FROM debian:latest
MAINTAINER Alexander Rozhkov "alex@voxlab.ru"
ENV DEBIAN_FRONTEND=noninteractive
#RUN apt-get install -y add-apt-repository
#RUN add-apt-repository "deb [arch=amd64] deb http://debian.ctm.ru/nightly/ stable main non-free"
#RUN wget -O - http://debian.ctm.ru/logs/repository_key.asc | sudo apt-key add -
#RUN apt-get update
#CMD ["/usr/bin/yate", "-vvv"]
#COPY yate /usr/src/yate
#COPY yate-extra /usr/src/yate-extra
RUN apt-get update && apt-get --yes --no-install-recommends install \
 libspeex1 libgsm1 libasound2 libsctp1 \
 build-essential pkg-config libasound2-dev ca-certificates \
 libpq-dev libssl-dev libgsm1-dev libspeex-dev \
 libspandsp-dev autoconf libsctp-dev libsqlite3-dev git \
 default-libmysqlclient-dev subversion
RUN svn checkout http://voip.null.ro/svn/yate/trunk /usr/src/yate
RUN cd /usr/src/yate \
 && ./autogen.sh \
 && ./configure --prefix=/usr --mandir=/usr/share/man --infodir=/usr/share/info --sysconfdir=/etc --disable-ilbc --enable-sctp \
 && make && make install-noapi
#RUN make install-noapi
RUN apt-get --yes remove build-essential
CMD ["/usr/bin/yate", "-vvv"]
