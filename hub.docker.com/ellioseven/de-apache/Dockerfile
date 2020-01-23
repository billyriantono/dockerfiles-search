FROM httpd:2.4
MAINTAINER elliot.mitchum@ellioseven.com

# Install global dependencies.
RUN apt-get update \
	&& apt-get install -y --no-install-recommends bash \
	&& rm -rf /var/lib/apt/lists/*;

# Create 'app' user.
RUN groupadd --gid 1000 app \
	&& useradd --uid 1000 --gid app --shell /bin/bash --create-home app \
	&& mkdir -p /home/app/src/docroot \
	&& mkdir -p /home/app/.local/opt \
	&& mkdir -p /home/app/bin \
	&& mkdir -p /home/app/.local/bin \
	&& mkdir -p /home/app/src/docroot \
	&& echo '. "$HOME/.bashrc"' >> /home/app/.profile \
	&& echo 'PATH=$HOME/bin:$PATH' >> /home/app/.bashrc \
	&& echo 'PATH=$HOME/src/docroot/vendor/bin:$PATH' >> /home/app/.bashrc \
	&& echo 'PATH=$HOME/.local/bin:$PATH' >> /home/app/.bashrc \
	&& chown -R app:app /home/app;

WORKDIR /home/app/src/docroot
ENV HTTPD_CONF /usr/local/apache2/conf/httpd.conf

# Set Apache user to 'app'.
RUN sed -i 's/User daemon/User app/' $HTTPD_CONF;

# Set Apache group to 'app'.
RUN sed -i 's/Group daemon/Group app/' $HTTPD_CONF;

# Enable rewrite module.
RUN sed -i 's/#LoadModule rewrite_module/LoadModule rewrite_module/' $HTTPD_CONF;

# Enable PHP-FPM.
RUN sed -i 's/#LoadModule proxy_module/LoadModule proxy_module/' $HTTPD_CONF;
RUN sed -i 's/#LoadModule proxy_fcgi_module/LoadModule proxy_fcgi_module/' $HTTPD_CONF;

# Enable virtual host configuration.
RUN sed -i 's/#Include conf\/extra\/httpd-vhosts.conf/Include conf\/extra\/httpd-vhosts.conf/' $HTTPD_CONF;

# Add virtual host configuration.
ADD httpd-vhosts.conf /usr/local/apache2/conf/extra/httpd-vhosts.conf

# Create default web root.
RUN mkdir -p /home/app/src/docroot \
    && echo '<?php phpinfo();' >> /home/app/src/docroot/index.php
