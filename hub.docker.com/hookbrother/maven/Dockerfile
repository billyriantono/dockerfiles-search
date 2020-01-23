FROM maven:3-jdk-8
MAINTAINER hookbrother <hookbrother@dingtalk.com>

# 保持运行状态
COPY run.sh /run.sh
RUN chmod 755 /*.sh

ENTRYPOINT ["/run.sh"]