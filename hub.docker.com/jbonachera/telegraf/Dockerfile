FROM jbonachera/arch
ENV VERSION=1.0.1
RUN curl https://dl.influxdata.com/telegraf/releases/telegraf-${VERSION}.x86_64.rpm | bsdtar -xC / -f - && \
    useradd -r telegraf -d /var/lib/telegraf/ 
COPY telegraf.conf /etc/telegraf/telegraf.conf
USER telegraf
CMD /usr/bin/telegraf
