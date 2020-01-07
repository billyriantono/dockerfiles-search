FROM alpine:3.7
MAINTAINER jackadam <jackadam@sina.com>

# 安装包源切到中科大, 国内访问加速
RUN { \
        echo 'http://mirrors.ustc.edu.cn/alpine/v3.7/main'; \
        echo 'http://mirrors.ustc.edu.cn/alpine/v3.7/community'; \
        echo 'http://mirrors.ustc.edu.cn/alpine/edge/main'; \
        echo 'http://mirrors.ustc.edu.cn/alpine/edge/community'; \
        echo 'http://mirrors.ustc.edu.cn/alpine/edge/testing'; \
    } > /etc/apk/repositories && \

# 设置默认时区为亚洲/上海 (没有北京可选)
	apk add --no-cache --upgrade apk-tools tzdata && \
	cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
	echo "Asia/Shanghai" > /etc/timezone && \
	apk del tzdata