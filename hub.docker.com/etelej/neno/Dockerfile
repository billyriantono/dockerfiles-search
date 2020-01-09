FROM node:stretch-slim
RUN apt-get update \
	&& apt-get install --no-install-recommends -y git \ 
	&& rm -rf /var/lib/apt/lists/*

COPY ./ /app/

WORKDIR /app

RUN git clone https://github.com/mozilla/readability.git ./readability \
	&& yarn

EXPOSE 3000

CMD ["yarn","serve"]

