FROM centos

RUN echo "[nginx]" > /etc/yum.repos.d/nginx.repo; \ 
echo "name=nginx repo" >> /etc/yum.repos.d/nginx.repo; \
echo "baseurl=http://nginx.org/packages/centos/7/`uname -m`/" >> /etc/yum.repos.d/nginx.repo; \
echo "gpgcheck=0" >> /etc/yum.repos.d/nginx.repo; \
echo "enabled=1" >> /etc/yum.repos.d/nginx.repo; \
yum update; \
yum search nginx; \
yum install -y 	nginx \
				ca-certificates \
				nginx-module-geoip \
				nginx-module-image-filter \
				nginx-module-njs \
				nginx-module-perl \
				nginx-module-xslt \
				gettext-base; \
yum clean all; \
rm -rf /var/lib/yum/*;

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;"]


