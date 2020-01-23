FROM ringcentral/jdk:8

RUN mkdir -p /usr/src/musicbot \
	&& curl https://api.github.com/repos/jagrosh/MusicBot/releases/latest \
	| grep "browser_download_url.*-Linux.jar" \
	| cut -d '"' -f 4 \
	| xargs wget -qO /usr/src/musicbot/musicbot.jar 

WORKDIR /usr/src/musicbot

CMD ["java", "-Dnogui=true", "-Dconfig.file=/usr/src/musicbot/config/config.txt", "-jar", "musicbot.jar"]
