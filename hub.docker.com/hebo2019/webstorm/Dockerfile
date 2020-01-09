FROM ubuntu

LABEL maintainer.name="hebo" maintainer.email="1113727572@qq.com"

ENV ID_PUB="none"

RUN apt update \
 && apt install -y openssh-server \
 && mkdir /root/.ssh \
 && sed -i "s/#X11UseLocalhost yes/X11UseLocalhost no/g" /etc/ssh/sshd_config \
 && echo '#!/bin/bash\n\
test -f /root/.ssh/authorized_keys || echo "$ID_PUB" > /root/.ssh/authorized_keys\n\
/etc/init.d/ssh start\n\
/bin/bash\n\
' > /entrypoint.sh && chmod +111 /entrypoint.sh

RUN apt install -y openjdk-11-jdk nodejs npm fonts-droid-fallback openjfx git \
 && npm i npm -g \
 && wget -P /root/tmp https://download.jetbrains.com/webstorm/WebStorm-2019.3.tar.gz \
 && mkdir /root/Webstorm && tar -C /root/Webstorm -axvf /root/tmp/WebStorm-2019.3.tar.gz \
 && rm -r /root/tmp \
 && ln -s /root/Webstorm/$(ls /root/Webstorm)/bin/webstorm.sh /usr/bin/webstorm

CMD ["/entrypoint.sh"]
