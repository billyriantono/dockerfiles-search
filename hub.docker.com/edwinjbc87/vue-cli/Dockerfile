FROM node:8.12.0

EXPOSE 8080

RUN npm i -g @vue/cli@3.4.1

VOLUME /usr/app/vuser
WORKDIR /usr/app/vuser

RUN apt-get update &&  \
	apt-get install nano &&  \
	useradd --create-home --shell /bin/bash vuser && \
    usermod -aG sudo vuser && \
    chown -R vuser:vuser /usr/app/vuser

USER vuser

CMD /bin/bash