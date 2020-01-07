FROM nginx:1.15
MAINTAINER EasycomLab <easycomlab@easycom.digital>

# =========================================
# Add the bashrc configuration
# =========================================
ADD ./bashrc.root /root/.bashrc

# =========================================
# RUN update
# =========================================
RUN apt-get update

# =========================================
# Install tools
# =========================================
RUN apt-get install -y \
    nano \
    vim \
    htop \
    iptraf \
    ssmtp \
    openssl \
    git

# =========================================
# Set ENV variables
# =========================================
ENV DEBUG false
ENV UPLOAD_MAX_FILESIZE 64M
ENV FPM_HOST fpm
ENV FPM_PORT 9000
ENV PROJECT_ROOT /var/www/htdocs

# =========================================
# Create generic SSL certificate
# =========================================
RUN cd /etc/ssl/certs && openssl req -subj '/CN=my.local/O=EasycomLab/C=FR' -new -newkey rsa:2048 -sha256 -days 365 -nodes -x509 -keyout server.key -out server.crt

# =========================================
# Add nginx.conf
# =========================================
ADD etc/nginx.conf /etc/nginx/nginx.conf

# =========================================
# Add vhosts
# =========================================
ADD etc/default.conf /etc/nginx/conf.d/default.conf
ADD etc/magento.conf /etc/nginx/conf.d/magento.conf
ADD etc/magento2.conf /etc/nginx/conf.d/magento2.conf
ADD etc/wordpress.conf /etc/nginx/conf.d/wordpress.conf
ADD etc/drupal8.conf /etc/nginx/conf.d/drupal8.conf
ADD etc/akeneo.conf /etc/nginx/conf.d/akeneo.conf
ADD etc/sf4.conf /etc/nginx/conf.d/sf4.conf

# =========================================
# Create easycom user
# =========================================
RUN openssl rand -base64 32 > ./.pass \
	&& useradd -ms /bin/bash --password='$(cat ./.pass)' easycom \
	&& adduser easycom ssh \
	&& echo "$(cat ./.pass)\n$(cat ./.pass)\n" | passwd easycom \
	&& mv ./.pass /home/easycom/ \
	&& chown -Rf easycom:easycom /home/easycom

#Add custom bashrc
ADD ./bashrc.easycom /home/easycom/.bashrc

# =========================================
# Install Pagespeed
# =========================================
RUN cd /root \
  && apt-get install -y uuid-dev wget g++ unzip gcc make libpcre3-dev zlib1g-dev \
  && NGINX_VERSION=$(v=$(nginx -v 2>&1) && echo -n $v | cut --delimiter='/' --fields=2) \
  && NPS_VERSION=1.13.35.2 \
  && wget -qO - http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz | tar zxfv - \
  && wget https://github.com/pagespeed/ngx_pagespeed/archive/v${NPS_VERSION}-stable.zip \
  && unzip v${NPS_VERSION}-stable.zip \
  && cd incubator-pagespeed-ngx-${NPS_VERSION}-stable/ \
  && psol_url=https://dl.google.com/dl/page-speed/psol/${NPS_VERSION}.tar.gz \
  && [ -e scripts/format_binary_url.sh ] && psol_url=$(scripts/format_binary_url.sh PSOL_BINARY_URL) \
  && wget ${psol_url} \
  && tar -xzvf $(basename ${psol_url}) \
  && cd ../nginx-${NGINX_VERSION} \
  && ./configure --add-dynamic-module=../incubator-pagespeed-ngx-${NPS_VERSION}-stable --with-compat \
  && make modules \
  && cp objs/ngx_pagespeed.so /etc/nginx/modules/

# =========================================
# Expose ports
# =========================================
EXPOSE 80
EXPOSE 443

ADD docker-entrypoint.sh /docker-entrypoint.sh
RUN ["chmod", "+x", "/docker-entrypoint.sh"]
ENTRYPOINT ["/docker-entrypoint.sh"]

WORKDIR $PROJECT_ROOT

CMD ["nginx", "-g", "daemon off;"]
