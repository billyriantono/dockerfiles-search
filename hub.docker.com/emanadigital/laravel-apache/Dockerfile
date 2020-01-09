# Apache Http with alpine
FROM httpd:2-alpine AS setup

# Update system
RUN apk update; \
    apk upgrade;

# Copy our website config to container
COPY ./website.apache.conf /usr/local/apache2/conf/website.apache.conf

# Tell apache to include our config
RUN echo "Include /usr/local/apache2/conf/website.apache.conf" \
    >> /usr/local/apache2/conf/httpd.conf

# Make public dir to bypass apache startup error
RUN mkdir -p /var/www/public/

# Make a volume to share project root
VOLUME [ "/var/www" ]

# Expose port 80
EXPOSE 80