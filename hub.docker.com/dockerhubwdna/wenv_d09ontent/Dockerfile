FROM nginx
RUN rm /etc/nginx/nginx.conf
COPY nginx.conf /etc/nginx

# Expose ports
EXPOSE 8080 443

#check if the config files are ok
#CMD nginx -t

# Set the default command to execute
# when creating a new container
CMD service nginx start
