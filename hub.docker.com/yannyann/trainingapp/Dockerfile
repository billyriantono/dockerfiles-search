FROM google/nodejs

WORKDIR /app
ADD package.json /app/
RUN npm install
ADD . /app
RUN npm install -g nodemon

EXPOSE 8080
CMD []
ENTRYPOINT ["/nodejs/nodemon","-x", "bin/www"]
