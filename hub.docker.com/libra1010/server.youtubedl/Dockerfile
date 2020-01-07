FROM libra1010/server.base:1.5
RUN curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
RUN chmod a+rx /usr/local/bin/youtube-dl
ADD ffmpeg-release-amd64-static.tar.xz /usr/local/bin/
ENV PATH /usr/local/bin/ffmpeg-4.1-64bit-static:$PATH