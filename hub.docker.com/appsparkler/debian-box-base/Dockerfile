FROM node:13.0.1

COPY .bashrc /root/.bashrc

# docker-image setup
COPY docker-image-setup.sh /bin/docker-image-setup.sh
RUN chmod +x /bin/docker-image-setup.sh
RUN "/bin/docker-image-setup.sh"

CMD ["/bin/bash", "-l"]
