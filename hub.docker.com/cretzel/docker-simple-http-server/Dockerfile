FROM debian
MAINTAINER cretzel

# Install nodejs
RUN apt-get update && apt-get install --yes curl
RUN curl --silent --location https://deb.nodesource.com/setup_0.12 | bash -
RUN apt-get install --yes nodejs
RUN apt-get install --yes build-essential

ADD src /simple-http-server
EXPOSE 8080
CMD node /simple-http-server/app.js
