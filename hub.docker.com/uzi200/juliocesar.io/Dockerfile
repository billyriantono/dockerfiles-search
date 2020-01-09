FROM debian:wheezy
MAINTAINER Julio César <julioc255io@gmail.com>
RUN apt-get update

# Install Nginx
RUN apt-get install -y nginx

# Download and install hugo
ENV HUGO_VERSION 0.14
ENV HUGO_BINARY hugo_${HUGO_VERSION}_linux_amd64

ADD https://github.com/spf13/hugo/releases/download/v${HUGO_VERSION}/${HUGO_BINARY}.tar.gz /usr/local/
RUN tar xzf /usr/local/${HUGO_BINARY}.tar.gz -C /usr/local/ \
    && ln -s /usr/local/${HUGO_BINARY}/${HUGO_BINARY} /usr/local/bin/hugo \
    && rm /usr/local/${HUGO_BINARY}.tar.gz


# Build the site
WORKDIR /usr/src/blog/
COPY . /usr/src/blog/
RUN hugo
RUN chmod +x -R /usr/src/blog/

# Configure Nginx
RUN rm /etc/nginx/sites-enabled/default
ADD nginx.conf /etc/nginx/sites-enabled/blog.conf

# Append "daemon off;" to the beginning of the configuration
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Expose ports
EXPOSE 80

# Set the default command to execute
# when creating a new container
CMD service nginx start
