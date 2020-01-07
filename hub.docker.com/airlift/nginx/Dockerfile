FROM nginx:1.15

# Update Nginx config
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

COPY conf/jupyter.conf /etc/nginx/conf.d/default.conf

# Expose port 80

EXPOSE 80

# Set the default command to execute

CMD ["nginx"]

