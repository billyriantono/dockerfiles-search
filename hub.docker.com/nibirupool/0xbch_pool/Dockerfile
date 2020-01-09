from node:8-stretch
RUN \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y curl vim wget git libsodium-dev libsodium18 less nano libboost-system-dev
COPY ./tokenpool /tokenpool
RUN \
  cd /tokenpool/ && \
  npm install &&\
  npm run webpack
 RUN \
  touch /var/pool.log &&\
  echo "#!/bin/bash\ncd /tokenpool && npm run server | tee --append /var/pool.log && bash" > /root/entry.sh &&\
  chmod +x /root/entry.sh
# VOLUME ["/root/ssl/"]
CMD ["/root/entry.sh"]
#CMD ["/bin/bash"]
