FROM "centos:latest"

# Copy build scripts
COPY --chown=root ./_scripts/ /

RUN chmod 555 /spargo/build/00-install_httpd.sh     
RUN /spargo/build/00-install_httpd.sh

RUN chmod 555 /spargo/run.sh

# Copy Configurations
COPY ./_configuration/ /

# Copy www directory
COPY ./www /spargo/www

WORKDIR /spargo/www
EXPOSE 80

ENTRYPOINT ["/spargo/run.sh"]