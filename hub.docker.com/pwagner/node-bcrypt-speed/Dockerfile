FROM node:4.2.3-slim

RUN apt-get update \
    && apt-get install -y \
	build-essential \
        python \
    && apt-get clean \
    && rm -Rf /var/lib/apt/lists/*

ADD package.json /app/

WORKDIR /app
RUN npm install --no-optional

ADD . /app/
ENTRYPOINT ["node","bcrypt-speed.js"]

