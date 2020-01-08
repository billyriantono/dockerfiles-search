## Update instructions
# To build: docker build -t motocom/pdf-to-jpg .
# To push: docker push motocom/pdf-to-jpg
# To run as daemon on port 8080: docker run --restart=always -p 8080:8080 -d motocom/pdf-to-jpg
##

# set our base for docker
FROM alpine:3.7

# install software using apk
RUN apk add --no-cache imagemagick ghostscript poppler-utils
RUN apk add --update nodejs

# install app dependencies with npm
COPY package.json /src/package.json
RUN cd /src; npm install

# copy the remainder of our files
COPY . /src

# expose port 8080
EXPOSE 8080

CMD ["node", "/src/app"]