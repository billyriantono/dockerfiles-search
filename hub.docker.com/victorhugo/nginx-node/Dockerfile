FROM victorhugo/nginx:latest
MAINTAINER VictorHugo <victorhugo.avila@easypoint.co>

RUN apt-get update && apt-get install -y \
						curl \
	&& curl -sL https://deb.nodesource.com/setup_5.x | bash - \
	&& apt-get install -y \
						apt-utils \
						nodejs \
						build-essential \
	&& rm -rf /var/lib/apt/lists/*

EXPOSE 80 443
CMD ["nginx", "-g", "daemon off;"]
