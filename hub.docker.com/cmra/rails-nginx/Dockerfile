FROM nginx

# install essential Linux packages
RUN apt-get update -qq && apt-get -y install apache2-utils

# establish where Nginx should look for files
ENV RAILS_ROOT /var/www/cs2n

# Set our working directory inside the image
WORKDIR $RAILS_ROOT

# create log directory
RUN mkdir log

# copy over static assets
COPY public public/

# custom 50x error file
COPY public/maintenance-notice.html /usr/share/nginx/html/custom_50x.html
RUN mkdir /etc/nginx/sites-enabled
COPY config/containers/sites-enabled /etc/nginx/sites-enabled/default

# copy our Nginx config template
COPY config/containers/nginx.conf /tmp/cs2n.nginx

# substitute variable references in the Nginx config template for real values from the environment
# put the final config in its place
RUN envsubst '$RAILS_ROOT' < /tmp/cs2n.nginx > /etc/nginx/conf.d/default.conf

# Use the "exec" form of CMD so Nginx shuts down gracefully on SIGTERM (i.e. `docker stop`)
CMD [ "nginx", "-g", "daemon off;" ]
