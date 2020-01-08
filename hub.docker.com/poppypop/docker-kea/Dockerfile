FROM alpine:edge

RUN echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories &&\
	apk add --update --no-cache tzdata bash curl mariadb-client \
		kea-dhcp4@testing kea-ctrl-agent@testing kea-admin@testing kea-hook-runscript@testing && \ 
	rm -rf /apk && rm -rf /var/cache/apk/*	

COPY hook.sh /hook.sh

ADD docker-entrypoint.sh /docker-entrypoint.sh
ADD kea-dhcp4.conf /etc/kea/kea-dhcp4.conf
ADD kea-ctrl-agent.conf /etc/kea/kea-ctrl-agent.conf

EXPOSE 67 67/udp
EXPOSE 8080

ENTRYPOINT [ "/docker-entrypoint.sh" ]
CMD [ "kea-dhcp4" ]
