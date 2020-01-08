FROM node:9.10.1

RUN mkdir /usr/src/app

WORKDIR /usr/src/app

COPY ./package*.json ./

RUN npm install

COPY . .

CMD if [ $NODE_ENV = 'production' ]; then \
    	npm install -g http-server && \
    	npm run build && \
      cd dist && \
    	hs -p 8080; \
  else \
     npm start;\
  fi
EXPOSE 8080
