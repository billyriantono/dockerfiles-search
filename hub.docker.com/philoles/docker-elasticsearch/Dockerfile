FROM docker.elastic.co/elasticsearch/elasticsearch-oss:6.2.4

RUN ./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.2.4/elasticsearch-analysis-ik-6.2.4.zip

ENV AUTH_REALM="elastic" \
    AUTH_HTPASSWD="song:vtdC8tHbU0saY" \
    AUTH_FORWARD_HOST="127.0.0.1" \
    AUTH_FORWARD_PORT=9200 \
    nginxversion="1.12.2-1" \
    os="centos" \
    osversion="7" \
    elversion="7_4"

COPY conf/nginx.conf /etc/nginx/nginx.conf
COPY conf/conf.d/* /etc/nginx/conf.d/
COPY docker-entrypoint.sh /docker-entrypoint.sh

RUN yum install -y wget openssl sed &&\
    yum -y install gettext && \
    yum -y autoremove &&\
    yum clean all &&\
    wget http://nginx.org/packages/$os/$osversion/x86_64/RPMS/nginx-$nginxversion.el$elversion.ngx.x86_64.rpm &&\
    rpm -iv nginx-$nginxversion.el$elversion.ngx.x86_64.rpm &&\
    mkdir -p /etc/nginx/conf.d && \
    chmod +x /docker-entrypoint.sh

EXPOSE 80

ENTRYPOINT ["/docker-entrypoint.sh"]
