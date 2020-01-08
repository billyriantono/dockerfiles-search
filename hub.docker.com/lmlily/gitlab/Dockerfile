FROM sameersbn/gitlab:12.1.0

ENV TZ="Asia/Shanghai"

RUN set -e \
&& apt-get update \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
&& echo $TZ > /etc/timezone \
&& apt-get install -y tzdata \
&& rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
