#Dockerfile
FROM fedora:26
MAINTAINER AlexaZhou <AlexaZhou@163.com>

#COPY 
COPY ./requirements.txt /root/image_info/

#install package
RUN yum install iputils net-tools openssl-static which -y && \
	yum install libsodium libsodium-static libsodium-devel -y && \	
    python3 -m pip --no-cache-dir install -r /root/image_info/requirements.txt && \
    yum clean all && \	
    rm -rf /tmp/*	

#End
