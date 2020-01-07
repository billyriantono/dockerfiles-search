#Version: 0.1.0
FROM centos
MAINTAINER WuHuixiong huixiongwu@gmail.com
RUN yum install gcc wget make xz readline-devel -y
RUN wget http://mirrors.sohu.com/python/3.4.3/Python-3.4.3.tar.xz
RUN xz -d Python-3.4.3.tar.xz && tar xf Python-3.4.3.tar
WORKDIR Python-3.4.3
RUN ./configure --prefix=/usr/local/python3 && make && make install
ENV PATH=$PATH:/usr/local/python3/bin
RUN mkdir -p /data
VOLUME ["/data"]
WORKDIR /data
CMD ["python3"]
