FROM centos:7

RUN yum install -y wget make gcc build-essential pcre pcre-devel perl zlib zlib-devel

RUN wget 'http://nginx.org/download/nginx-1.7.10.tar.gz'
RUN wget 'https://github.com/openresty/headers-more-nginx-module/archive/v0.261.tar.gz'
RUN tar -xzvf nginx-1.7.10.tar.gz
RUN tar -xzvf v0.261.tar.gz
WORKDIR nginx-1.7.10/
RUN ./configure --prefix=/opt/nginx --add-module=../headers-more-nginx-module-0.261/
RUN make
RUN make install

EXPOSE 80

CMD ["/opt/nginx/sbin/nginx", "-g", "daemon off;"]
