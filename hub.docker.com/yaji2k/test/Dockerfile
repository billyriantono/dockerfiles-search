FROM alpine

RUN apk add git \
	&& apk add npm \
	&& git clone https://github.com/yaji2k/vue-product-card.git \
	&& cd vue-product-card \
	&& npm i

WORKDIR ./vue-product-card

CMD npm run serve

EXPOSE 8080
