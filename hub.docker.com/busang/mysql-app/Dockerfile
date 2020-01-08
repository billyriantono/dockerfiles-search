FROM mysql:5.7

ENV TZ=Asia/Shanghai

RUN apt update && apt install -y tzdata \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone
