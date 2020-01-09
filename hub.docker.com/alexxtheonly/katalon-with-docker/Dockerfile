FROM katalonstudio/katalon:7.1.0

RUN wget -O docker.tgz https://download.docker.com/linux/static/stable/x86_64/docker-19.03.5.tgz

RUN tar --extract \
		--file docker.tgz \
		--strip-components 1 \
		--directory /usr/local/bin/ \
	; \
	rm docker.tgz; \
	\
	dockerd --version; \
	docker --version

COPY modprobe.sh /usr/local/bin/modprobe
COPY entrypoint.sh /usr/local/bin/

RUN chmod 775 /usr/local/bin/entrypoint.sh

RUN mkdir /certs /certs/client && chmod 1777 /certs /certs/client

ENTRYPOINT ["entrypoint.sh"]