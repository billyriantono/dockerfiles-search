FROM adi90x/rancher-active-proxy:latest

RUN { \
    	echo 'server_tokens off;'; \
		echo 'proxy_connect_timeout 3000;'; \
		echo 'proxy_send_timeout 3000;'; \
		echo 'proxy_read_timeout 3000;'; \
		echo 'client_header_timeout 3000;'; \
		echo 'client_body_timeout 3000;'; \
		echo 'client_max_body_size 100m;'; \
		echo 'fastcgi_buffers 8 128k;'; \
		echo 'fastcgi_buffer_size 128k;'; \
		echo 'fastcgi_read_timeout 3000;'; \
    } > /etc/nginx/conf.d/custom_proxy.conf
