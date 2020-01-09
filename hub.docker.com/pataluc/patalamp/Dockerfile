FROM tutum/lamp:latest
RUN rm -fr /app && git clone https://github.com/pataluc/my-conf.git
VOLUME /app
EXPOSE 80 3306
CMD ["/run.sh"]
