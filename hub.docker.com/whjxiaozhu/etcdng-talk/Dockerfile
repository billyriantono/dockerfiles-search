FROM openjdk:8u92-alpine
MAINTAINER web-xiaxia<xiongchuang@vip.qq.com>

#设置环境变量
ENV DINGDING_TOKEN=${TOKEN} \
    DINGDING_MSGKEY=Alarm \
    SKYWALKING_WEBHOOK_WORK_SPACE=/skywalking/webhook \
    APP_JAR_NAME=skywalking-webhook-dingding-talk-jar-with-dependencies.jar


#执行需要的内容
RUN mkdir ${SKYWALKING_WEBHOOK_WORK_SPACE} -p 

#复制内容
COPY ${APP_JAR_NAME} ${SKYWALKING_WEBHOOK_WORK_SPACE}

#复制启动脚本
COPY start.sh /bin/

#执行权限
RUN chmod 777 /bin/start.sh

#工作空间
WORKDIR ${SKYWALKING_WEBHOOK_WORK_SPACE}
EXPOSE 8080
ENTRYPOINT ["/bin/start.sh"]
