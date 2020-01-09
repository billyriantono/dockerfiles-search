FROM nginx

MAINTAINER Ruslan Shevchenko "galucinogen@gmail.com"

RUN apt-get update && apt-get -y install git zlib1g-dev libpcre3 libpcre3-dev make gcc wget mc && mkdir /home/test && cd /home/test && \
git clone http://luajit.org/git/luajit-2.0.git && cd /home/test/luajit-2.0 && make && make install && cd .. && wget https://github.com/simplresty/ngx_devel_kit/archive/v0.3.0.tar.gz && tar -xzf v0.3.0.tar.gz && \
wget https://github.com/openresty/lua-nginx-module/archive/v0.10.11.tar.gz && tar -xzf v0.10.11.tar.gz && \
export LUAJIT_LIB=/usr/local/lib && export LUAJIT_INC=/usr/local/include/luajit-2.0 && \
wget http://nginx.org/download/nginx-1.13.8.tar.gz && tar -xzf nginx-1.13.8.tar.gz && cd /home/test/nginx-1.13.8 && \
./configure --prefix=/opt/nginx --with-ld-opt="-Wl,-rpath,/usr/local/lib" --add-module=/home/test/ngx_devel_kit-0.3.0 --add-module=/home/test/lua-nginx-module-0.10.11 && make -j2 && make install && \
mv /usr/sbin/nginx /usr/sbin/nginx1 && ln -s /opt/nginx/sbin/nginx /usr/sbin/nginx


RUN cd /home/test && git clone http://github.com/Galucinogen/test_nginx.git
RUN cp /home/test/test_nginx/conf/nginx.conf /opt/nginx/conf/nginx.conf && cp /home/test/test_nginx/html/index.html /opt/nginx/html/index.html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
