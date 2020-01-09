FROM amazonlinux:2
EXPOSE 8888
ADD requirements.txt /
RUN yum install -y -q wget shadow-utils yum-utils && \
	useradd -d /opt/deployment phenom -u 1004 && \
	wget -q -O /tmp/get-pip.py https://bootstrap.pypa.io/get-pip.py && \
    chmod a+x /tmp/get-pip.py && \
    /tmp/get-pip.py && \
    mkdir -p /opt/deployment/thumbor/logs && \
    touch /opt/deployment/thumbor/logs/thumbor.log && \
    chown -R phenom:phenom /opt/deployment
RUN pip install  -r requirements.txt
ADD thumbor.conf /etc/thumbor.conf
ADD start-server.sh /opt/deployment/start-server.sh
RUN  yum update --security -q -y
RUN package-cleanup --oldkernels --count=1 -y -q
USER phenom
ENTRYPOINT ["/opt/deployment/start-server.sh"]
