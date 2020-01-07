FROM mongo:4.0.10-xenial

ENV TZ="Asia/Shanghai"

RUN set -e \
&& apt-get update \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
&& echo $TZ > /etc/timezone \
&& apt-get install -y tzdata \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
