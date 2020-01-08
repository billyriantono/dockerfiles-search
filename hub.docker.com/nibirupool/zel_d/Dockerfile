#Dockerfile for zelcash daemon.
FROM nibirupool/nibiru:latest
RUN \
	# pull
	git clone https://github.com/zelcash/zelcash.git && \
	cd zelcash  && \
	# fetch key
	./zcutil/fetch-params.sh && \
	# Build
	./zcutil/build.sh -j$(nproc)
COPY ./blocknotify.c /var/
RUN cd /var && gcc blocknotify.c -o blocknotify && mv /var/blocknotify /bin && rm /var/blocknotify.c
RUN \
  mkdir /root/.zelcash
RUN \
  echo "#!/bin/bash\n/zelcash/src/zelcashd && bash" > /root/entry.sh &&\
  chmod +x /root/entry.sh
VOLUME ["/root/.zelcash"]
COPY ./zelcash.conf /root/.zelcash/zelcash.conf
ENTRYPOINT ["/root/entry.sh"]
