FROM nginx:latest

RUN { \
		echo 'http {'; \
		echo '	stream {'; \
		echo '		server {'; \
		echo '			listen 80;'; \
		echo '			server_name */mysql;'; \
		echo '			proxy_connect_timeout 1s;'; \
		echo '			proxy_timeout 3s;'; \
		echo '			proxy_pass mysql-56-server.development;'; \
		echo '		}'; \
		echo '	}'; \
		echo '}'; \
	} > /etc/nginx/conf.d/server.conf

EXPOSE 80
CMD ["nginx"]
