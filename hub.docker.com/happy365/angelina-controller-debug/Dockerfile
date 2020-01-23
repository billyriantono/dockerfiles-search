FROM centos:7.3.1611
ENV VERSION 2.0
ENV BaseUrl http://files.happy366.cn/files/docker
RUN yum install epel-release -y
RUN yum install wget git -y
EXPOSE 6300
RUN wget -c $BaseUrl/angelina2/bin/angelina-controller -O /usr/bin/angelina-controller  && \
	wget -c $BaseUrl/angelina2/bin/angelina-runner   -O /root/angelina-runner && \
	wget -c $BaseUrl/angelina2/utils/redis-cli   -O /usr/bin/redis-cli  && \
	wget -c $BaseUrl/angelina2/utils/socket_client -O /usr/bin/socket_client && \
	wget -c $BaseUrl/angelina2/utils/angelina-runner-pod.yml -O /root/angelina-runner-pod.yml && \
	wget -c $BaseUrl/testdoc.sh -O /usr/bin/testdoc.sh
RUN chmod +x /usr/bin/angelina-controller && \
	chmod +x /usr/bin/redis-cli && \
	chmod +x /usr/bin/socket_client && \
	rm -rf /etc/localtime && \
	ln -sv /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
ENTRYPOINT ["/bin/bash","/usr/bin/testdoc.sh"]
