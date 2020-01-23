FROM hebo2019/ssh

ENV VERSION="2019.3.1"

RUN apt update \
 && apt install -y openjdk-11-jdk openjdk-11-source openjdk-11-doc fonts-droid-fallback openjfx git nodejs npm \
 && npm i npm -g \
 && wget -P /root/tmp https://download.jetbrains.com/webstorm/WebStorm-"${VERSION}".tar.gz \
 && mkdir /root/Webstorm && tar -C /root/Webstorm -axvf /root/tmp/WebStorm-"${VERSION}".tar.gz \
 && rm -r /root/tmp \
 && ln -s /root/Webstorm/$(ls /root/Webstorm)/bin/webstorm.sh /usr/bin/webstorm

CMD ["/entrypoint.sh"]
