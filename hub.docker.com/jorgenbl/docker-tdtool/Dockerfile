FROM python:2

RUN pip install oauth ConfigObj
RUN pip install paho-mqtt

RUN wget https://raw.githubusercontent.com/jorgenbl/telldus/master/examples/python/live/tdtool/tdtool.py
RUN apt-get update && apt-get install -y cron openssh-server
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
COPY telldus-cron /etc/cron.d/telldus-cron
COPY cron.sh /cron.sh

EXPOSE 22

#CMD ["./cron.sh"]
ENTRYPOINT service ssh start && ./cron.sh
