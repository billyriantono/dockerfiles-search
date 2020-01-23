FROM openjdk:12
RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
 && yum install -y xz GraphicsMagick \
 && mkdir /usr/src/ffmpeg \
 && cd /usr/src/ffmpeg \
 && curl -o ffmpeg.tar.xz https://johnvansickle.com/ffmpeg/releases/ffmpeg-release-amd64-static.tar.xz \
 && tar xf ffmpeg.tar.xz --strip-components=1 \
 && mv ffmpeg ffprobe /usr/local/bin \
 && cd /; rm -rf /var/cache/yum /usr/src/ffmpeg
