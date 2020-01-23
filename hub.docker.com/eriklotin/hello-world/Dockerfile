FROM busybox:latest

COPY index.html /var/www
COPY run.sh /
RUN chmod +r /run.sh

EXPOSE 80

ENTRYPOINT ["sh"]

CMD ["/run.sh"]