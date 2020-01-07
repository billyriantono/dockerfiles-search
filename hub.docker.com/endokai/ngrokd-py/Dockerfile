FROM ubuntu:16.04
MAINTAINER endokai
ENV domain ngrok.com
ADD https://github.com/hauntek/python-ngrokd/archive/master.zip /tmp/python-ngrokd.zip
ADD run.sh /tmp/run.sh
EXPOSE 80 443 4443 
RUN set -ex \
   && cd /tmp \
   && apt update && apt install zip python3 -y \
   && unzip /tmp/python-ngrokd.zip \
   && install -v -D /tmp/python-ngrokd-master/connt.py /root/connt.py \
   && install -v -D /tmp/python-ngrokd-master/msg.py /root/msg.py \
   && install -v -D /tmp/python-ngrokd-master/ngrokd.py /root/ngrokd.py \
   && install -v -D /tmp/python-ngrokd-master/snakeoil.crt /root/snakeoil.crt \
   && install -v -D /tmp/python-ngrokd-master/snakeoil.key /root/snakeoil.key \
   && install -v -D /tmp/run.sh /root/run.sh  \
   && chmod +x /root/run.sh && cd /root
ENTRYPOINT ["/root/run.sh"]
CMD ["/root/run.sh","$domain"]
