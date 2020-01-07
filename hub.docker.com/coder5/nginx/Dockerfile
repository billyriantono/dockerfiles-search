FROM ubuntu:14.04
ENV UPDATE_AT 20171205
RUN apt-get update
RUN sudo apt-get install -y build-essential
RUN sudo apt-get install -y libpcre3 libpcre3-dev 
RUN apt-get install -y  zlib1g-dev libssl-dev
RUN apt-get install  -y wget
RUN mkdir -p /source/nginx
WORKDIR /source
RUN wget http://nginx.org/download/nginx-1.12.2.tar.gz -O nginx.tar.gz
RUN tar -xvf nginx.tar.gz -C /source/nginx
WORKDIR /source/nginx/nginx-1.12.2
RUN ./configure --with-http_ssl_module --with-http_v2_module
RUN make && make install
#ADD conf/ /usr/local/nginx/conf/
EXPOSE 80
EXPOSE 443
