FROM node:8.5-alpine
RUN apk --no-cache add git
RUN npm install -g gitbook-cli@2.3.2 
RUN gitbook fetch 3.2.3
WORKDIR /mathjax
RUN echo '{"plugins":["mathjax@1.1.2"]}' > book.json && gitbook install && rm -rf book.json
VOLUME /book
WORKDIR /book
