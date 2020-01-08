FROM phusion/passenger-nodejs:1.0.8
MAINTAINER Szorfein <szorfein@protonmail.com>

# env
ENV HOME /root
ARG URL
ENV PROJECT_URL=${URL:-https://github.com/szorfein/vuejs-webapp}

CMD ["/sbin/my_init"]

# Enable Nginx
RUN rm -f /etc/service/nginx/down
RUN rm /etc/nginx/sites-enabled/default
ADD webapp.conf /etc/nginx/sites-enabled/webapp.conf

# Download your app
RUN mkdir -p /home/app
RUN git clone $PROJECT_URL /home/app/webapp

# Set permission on webapp
RUN usermod -u 1000 app
RUN chown -R app:app /home/app/webapp

# npm install (better to build an independent layer)
WORKDIR /tmp
RUN cp /home/app/webapp/package*.json .
RUN npm install
RUN cp -a node_modules /home/app/webapp/

# Generate the dist dir for the production
WORKDIR /home/app/webapp

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 80

COPY cmd.sh /cmd.sh
CMD ["/cmd.sh"]
