FROM ubuntu:18.04

ENV APP_LIMIT=4 \
    INTERVAL=15

ADD run.sh /root/run.sh

RUN \
  # Update Cache
  apt-get update && \
  # Install packages
  apt-get install adb -y && \
  ## Cleanup
  apt-get clean && \
  rm -rf \
	/tmp/* \
	/var/tmp/* && \
  rm -rf /var/lib/apt/lists/*

CMD /root/run.sh $TV_IP $APP_LIMIT $INTERVAL
