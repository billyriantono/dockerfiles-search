#Dockerfile for komodo daemon.
from nibirupool/nibiru:latest
RUN \
  git clone https://github.com/litecoinz-project/litecoinz.git
WORKDIR /litecoinz 
RUN \
  ./zcutil/build.sh
COPY ./blocknotify.c /var/
RUN cd /var && gcc blocknotify.c -o blocknotify && mv /var/blocknotify /bin && rm /var/blocknotify.c
RUN \
  mkdir /root/.litecoinz &&\
  echo "#!/bin/bash\n/usr/bin/litecoinzd && bash" > /root/entry.sh &&\
  chmod +x /root/entry.sh
VOLUME ["/root/.litecoinz"]
ADD ./litecoinz.conf /root/.litecoinz/litecoinz.conf
ENTRYPOINT ["/root/entry.sh"]
