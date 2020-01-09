# 基础镜像
FROM ryaning/tomcat:8-jre8
# 作者
MAINTAINER  ryan <me@ryana.cn>
# 变量
ENV JPDA_ADDRESS="8000"
ENV JPDA_TRANSPORT="dt_socket"
# 容器运行时监听的端口
EXPOSE 8080 8000
# 启动时运行
ENTRYPOINT ["catalina.sh", "jpda", "run"]
