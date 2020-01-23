FROM rsyslog/syslog_appliance_alpine

RUN apk --no-cache update && apk --no-cache add openssh expect zip
RUN sed -i -e '2icrond' /home/appliance/starter.sh
