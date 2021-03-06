# ref: http://www.inmethod.com/forum/posts/list/1856.page

FROM ubuntu:14.04

MAINTAINER nacat78 <nacat78@gmail.com.com>

ENV DEBIAN_FRONTEND noninteractive

RUN locale-gen en_US en_US.UTF-8

ADD multiverse.sources.list /etc/apt/sources.list.d/

RUN apt-get update
RUN apt-get -y upgrade

# dependicies of airvideo
RUN apt-get -y --no-install-recommends install libmp3lame0 libx264-dev libfaac0 faac openjdk-6-jre avahi-daemon

# install fonts
RUN apt-get -y --no-install-recommends install ttf-wqy-microhei fonts-dejavu

# curl
RUN apt-get -y --no-install-recommends install curl

# airvideo server's files
ADD AirVideoServerLinux.properties /opt/airvideo-server/
ADD airvideo-server.service /etc/avahi/services/
ADD airvideo-server /usr/bin/
RUN mkdir -p /opt/airvideo-server/bin
RUN curl -s http://s3.amazonaws.com/AirVideo/Linux-2.4.6-beta3/AirVideoServerLinux.jar -o /opt/airvideo-server/AirVideoServerLinux.jar

# compile avconv
RUN apt-get install -y build-essential libmp3lame-dev libfaac-dev yasm pkg-config && \
	    cd /tmp && \
	    curl -s http://s3.amazonaws.com/AirVideo/Linux-2.4.6-beta3/libav.tar.bz2 -o libav.tar.bz2 && \
	    tar xf libav.tar.bz2 && \
	    cd libav && \
	    ./configure --enable-pthreads --disable-shared --enable-static --enable-gpl --enable-libx264 --enable-libmp3lame --enable-nonfree --enable-libfaac && \
	    make -j4 && \
	    strip -s -o /opt/airvideo-server/bin/avconv /tmp/libav/avconv && \
	    apt-get purge -y build-essential libmp3lame-dev libfaac-dev yasm pkg-config && \
	    apt-get autoremove -y && \
	    apt-get autoclean && \
	    rm -rf /tmp/libav.tar.bz2 /tmp/libav
	   

# run as nobody instead of root & fix permissions  
RUN usermod -u 99 nobody
RUN usermod -g 100 nobody
RUN chown -R nobody:users /opt/airvideo-server

CMD java -jar /opt/airvideo-server/AirVideoServerLinux.jar /opt/airvideo-server/AirVideoServerLinux.properties
