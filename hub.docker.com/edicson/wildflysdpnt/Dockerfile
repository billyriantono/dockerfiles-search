FROM node:lts

RUN mkdir -p /app/node_modules && chown -R node:node /app
WORKDIR /app

RUN apt-get update \
	&& apt-get install -y libgtk2.0-0 libnotify-dev libgconf-2-4 libnss3 libxss1 libasound2 xvfb python-pip \
	&& apt-get clean
RUN pip install awscli --upgrade
