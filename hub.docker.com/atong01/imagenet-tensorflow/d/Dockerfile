FROM atline/dpmbase:0.1.0

ENV DP_VERSION v0.7.0

# define working directory
WORKDIR /root

# install dpm
RUN set -eux; \
  wget https://github.com/atline/dapeng/releases/download/$DP_VERSION/dpm.tar.bz2 && \
  tar jxvf dpm.tar.bz2 && \
  chmod -R 777 dpm && \
  rm -fr dpm.tar.bz2

CMD ["dpm/bin/dpm"]
