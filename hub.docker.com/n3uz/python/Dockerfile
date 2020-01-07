#A python2.7.15 in the GFW
FROM python:2.7.15-jessie

#Apply apt source with aliyun mirror
RUN sed -i 's/deb.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    sed -i 's/security.debian.org/mirrors.aliyun.com/g' /etc/apt/sources.list

#modify tzdata
RUN apt-get update && \
    apt-get install vim mlocate tzdata -y
RUN rm -fr /etc/localtime && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
	
#modify pip mirror with douban.com
RUN pip install alerta -i http://pypi.douban.com/simple --trusted-host pypi.douban.com

RUN pip install --upgrade pip

COPY bashrc /etc/bash.bashrc

WORKDIR /root

CMD /bin/bash
