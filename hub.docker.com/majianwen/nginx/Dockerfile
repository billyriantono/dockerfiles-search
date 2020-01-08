# base image
FROM centos

# put nginx-1.12.2.tar.gz into /usr/local/src and unpack nginx
#ADD http://nginx.org/download/nginx-1.12.2.tar.gz /usr/local/src

# running required command
RUN yum install -y gcc gcc-c++ glibc make autoconf openssl openssl-devel wget
RUN yum install -y libxslt-devel -y gd gd-devel GeoIP GeoIP-devel pcre pcre-devel
RUN useradd -M -s /sbin/nologin nginx
RUN cd /usr/local && wget http://nginx.org/download/nginx-1.12.2.tar.gz && tar zxvf nginx-1.12.2.tar.gz

# change dir to /usr/local/src/nginx-1.12.2
#WORKDIR /usr/local/src/nginx-1.12.2

# execute command to compile nginx
RUN cd /usr/local/nginx-1.12.2 && ./configure --user=nginx --group=nginx --prefix=/usr/local/nginx --with-file-aio  --with-http_ssl_module  --with-http_realip_module    --with-http_addition_module    --with-http_xslt_module   --with-http_image_filter_module    --with-http_geoip_module  --with-http_sub_module  --with-http_dav_module --with-http_flv_module    --with-http_mp4_module --with-http_gunzip_module  --with-http_gzip_static_module  --with-http_auth_request_module  --with-http_random_index_module   --with-http_secure_link_module   --with-http_degradation_module   --with-http_stub_status_module && make && make install

ENV PATH /usr/local/nginx/sbin:$PATH

EXPOSE 80
