FROM alpine:3.3
#MAINTAINER Advantech

RUN apk update \
  && apk add --no-cache git bash nodejs python python-dev py-pip && \
  git clone https://github.com/Vincent-Chu/hdd-ml-test.git /home/adv/hdd_failure_predict && \
  /bin/chmod a+w /home/adv/hdd_failure_predict/Feature.data && /bin/cp /home/adv/hdd_failure_predict/start.sh /usr/local/bin/. && \
  /bin/chmod a+rwx -R /home/adv/hdd_failure_predict/ && \
  /bin/rm -rf /tmp/* /var/cache/apk/*
  
WORKDIR /home/adv
ENTRYPOINT ["start.sh"]

