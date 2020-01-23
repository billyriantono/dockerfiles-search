FROM alpine:latest
USER root
RUN apk add --update --no-cache \
  ffmpeg ffmpeg-libs x264 x265 procps npm curl python2 make \
	xf86-video-amdgpu \
	xf86-video-intel \
	libva \
	mesa-dri-ati \
  && npm install pm2 -g \
  && npm cache verify \
  && curl -s https://gitlab.com/Shinobi-Systems/Shinobi/-/archive/master/Shinobi-master.tar.gz -o /tmp/shinobi.tar.gz \
  && cd /tmp/ \
  && tar -xzf shinobi.tar.gz \
  && mv Shinobi-master /opt/shinobi \
  && rm -rf /tmp/* \
  && adduser -u 1000 -S node -G users \
  && chmod -R 755 /opt/shinobi \
  && chown -R node:users /opt/shinobi
USER node
VOLUME ["/opt/shinobi/videos"]
WORKDIR /opt/shinobi
RUN cp conf.sample.json conf.json \
  && npm install \
  && npm cache verify \
  && cp super.sample.json super.json
CMD ["pm2-runtime,"start","camera.js"]
