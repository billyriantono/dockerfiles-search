FROM alpine
MAINTAINER Phill93 <mail@phill93.de>
EXPOSE 7072 8083 8084 8085
VOLUME /opt/fhem/config
VOLUME /opt/fhem/log

# Install Requirments
RUN apk add --update perl perl-device-serialport perl-crypt-rijndael sudo && \
rm -rf /var/cache/apk/* && \
adduser -S -D -h /opt/fhem -G dialout fhem && \
cd /opt/fhem && sudo -u fhem -s /bin/ash && \
wget http://fhem.de/fhem-5.7.tar.gz && \
tar -xzf fhem-5.7.tar.gz -C /tmp/ && \
rm fhem-5.7.tar.gz && \
cp -R /tmp/fhem-5.7/* ./ && \
rm -r /tmp/fhem-5.7/

ADD startup.sh /opt/fhem/startup.sh
#ADD config/fhem.cfg /opt/fhem/

RUN chmod a+x /opt/fhem/startup.sh && chown -R fhem:dialout /opt/fhem/

ENTRYPOINT /opt/fhem/startup.sh
