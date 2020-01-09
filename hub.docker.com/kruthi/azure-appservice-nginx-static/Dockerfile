FROM nginx:1.13

# Install openssh-server to provide web ssh access from kudu, supervisor to run processor
RUN apt-get update \
    && apt-get install --no-install-recommends --no-install-suggests -y \
    supervisor \
    openssh-server \
    && echo "root:Docker!" | chpasswd	

COPY nginx.conf /etc/nginx/nginx.conf
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf	
COPY sshd_config /etc/ssh/
COPY init_container.sh /bin/
RUN mkdir -p /home/site/wwwroot/dist
COPY dist /home/site/wwwroot/dist

EXPOSE 80 2222
CMD ["/bin/init_container.sh"]
