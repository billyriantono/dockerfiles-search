FROM ubuntu:trusty

ENV OS_LOCALE="en_US.UTF-8"
RUN locale-gen ${OS_LOCALE}

# Add entrypoint script to image
COPY entrypoint.sh /sbin/entrypoint.sh

RUN     \
        chmod 755 /sbin/entrypoint.sh

EXPOSE 80

CMD ["/sbin/entrypoint.sh"]