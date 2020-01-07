FROM alpine:3.4
MAINTAINER garywlee@gmail.com

# Install system package.
RUN apk add --no-cache bash
RUN apk add --no-cache nodejs

# Install node modules.
RUN npm install -g npm-cache
RUN npm install -g bower
RUN npm install -g webpack
RUN npm install -g gulp
RUN npm install -g grunt

# Allow bower to be executed with root privilege in container.
RUN echo '{ "allow_root": true }' > /root/.bowerrc

# Create folder for application.
RUN mkdir /app
WORKDIR /app

# Set default command
CMD ["bash"]

