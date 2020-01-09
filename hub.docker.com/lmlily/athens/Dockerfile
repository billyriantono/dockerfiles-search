FROM gomods/athens:v0.5.0

ENV TZ=Asia/Shanghai

RUN set -e \
&& apk add --no-cache tzdata \
&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
&& echo $TZ > /etc/timezone
