FROM alpine:edge

# Install Node
RUN apk add nodejs

# Install Yarn
RUN apk add yarn

# Copy app to /src
COPY . /src

# Install app and dependencies into /src
RUN cd /src; yarn install

EXPOSE 8080

CMD cd /src && node ./app.js
