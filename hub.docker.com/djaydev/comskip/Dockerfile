FROM alpine:3.11

WORKDIR /tmp

RUN apk --no-cache add python ffmpeg tzdata bash \
&& apk --no-cache add --virtual=builddeps autoconf automake libtool git ffmpeg-dev wget tar build-base \
&& wget http://prdownloads.sourceforge.net/argtable/argtable2-13.tar.gz \
&& tar xzf argtable2-13.tar.gz \
&& cd argtable2-13/ && ./configure && make && make install \
&& cd /tmp && git clone git://github.com/erikkaashoek/Comskip.git \
&& cd Comskip && ./autogen.sh && ./configure && make && make install \
&& wget -O /opt/PlexComskip.py https://raw.githubusercontent.com/ekim1337/PlexComskip/master/PlexComskip.py \
&& wget -O /opt/PlexComskip.conf https://raw.githubusercontent.com/ekim1337/PlexComskip/master/PlexComskip.conf.example \
&& sed -i "s#/usr/local/bin/ffmpeg#/usr/bin/ffmpeg#g" /opt/PlexComskip.conf \
&& sed -i "/forensics/s/True/False/g" /opt/PlexComskip.conf \
&& apk del builddeps \
&& rm -rf /var/cache/apk/* /tmp/* /tmp/.[!.]*

COPY --from=plexinc/pms-docker /usr/lib/plexmediaserver/Resources/comskip.ini /opt/comskip.ini

ENTRYPOINT [ "python", "/opt/PlexComskip.py" ]