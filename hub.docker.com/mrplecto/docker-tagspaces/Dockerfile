
FROM nginx


ENV TAGSPACES_VERSION 3.1.4


RUN apt-get update

RUN apt-get install -y wget unzip

RUN rm -rf /var/lib/apt/lists/*

RUN wget https://github.com/tagspaces/tagspaces/releases/download/v${TAGSPACES_VERSION}/tagspaces-web.zip

RUN unzip tagspaces-web.zip

RUN rm -rf /usr/share/nginx/html

RUN mv web /usr/share/nginx/html

RUN rm -rf tagspaces-web.zip


EXPOSE 80

VOLUME /usr/share/nginx/html/data


