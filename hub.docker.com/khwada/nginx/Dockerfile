FROM ubuntu
RUN apt-get update

RUN apt-get install -y nginx
# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log
# Remove the default Nginx configuration file
RUN rm -v /etc/nginx/nginx.conf
# Copy a configuration file from the current directory
ADD nginx.conf /etc/nginx/
# Expose ports
EXPOSE 80
# Set the default command to execute when creating a new container
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
