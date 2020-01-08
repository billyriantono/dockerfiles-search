#Dockerfile for Zcash daemon.
FROM nibirupool/nibiru:latest
RUN \
  git clone https://github.com/zcash/zcash.git &&\
  cd zcash && ./zcutil/build.sh
COPY ./blocknotify.c /var/
RUN cd /var && gcc blocknotify.c -o blocknotify && mv /var/blocknotify /bin && rm /var/blocknotify.c
RUN \
  /zcash/zcutil/fetch-params.sh &&\
  echo "#!/bin/bash\n/zcash/src/zcashd && bash" > /root/entry.sh &&\
  chmod +x /root/entry.sh 
VOLUME ["/root/.zcash"]
COPY ./zcash.conf /root/.zcash/zcash.conf
ENTRYPOINT ["/root/entry.sh"]
