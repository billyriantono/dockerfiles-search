FROM eoogo/ubuntu
WORKDIR /var/www/
ENTRYPOINT ["/bin/devt-init.sh"]
COPY devt-init.sh /bin/
VOLUME "/var/www/"
RUN chmod +x /bin/devt-init.sh
