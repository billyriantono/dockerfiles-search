FROM nathonfowlie/centos-jre

USER root
ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
	&& yum -y update \
	&& yum clean all \
	&& rm -rf /var/cache/yum \
	&& mkdir -p /data

ENTRYPOINT ["java", "-jar", "/data/runjar.jar"]
