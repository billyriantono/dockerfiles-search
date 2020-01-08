FROM nginx
MAINTAINER him_aeng@yahoo.co.th

ARG DEBIAN_FRONTEND=noninteractive
ENV TERM xterm

# Copy nginx config files
COPY default.conf /etc/nginx/conf.d/

# Update and install some useful apts
RUN apt-get update

# Install curl
RUN apt-get install -y curl

# Install node and npm
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs
RUN apt-get install -y build-essential

# Copy javascript files
RUN mkdir -p /usr/share/nginx/source
COPY . /usr/share/nginx/source

# Set permission for root document
RUN chmod -R 755 /usr/share/nginx/html/

# Go into root document to run npm install
WORKDIR /usr/share/nginx/source
RUN npm install

# Build project
RUN npm run build

# Copy build files to root document
RUN cp -r build/* /usr/share/nginx/html

# Check the content of build
RUN ls -la /usr/share/nginx/html/

# expose port 80
EXPOSE 80
