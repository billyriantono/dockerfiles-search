FROM tutum/lamp:latest
RUN rm -fr /app && git clone https://github.com/gabrielecirulli/2048.git /app
RUN sed -i "s/<title>2048<\/title>/<title>GIT-2048-$(date)<\/title>/g" /app/index.html
EXPOSE 80 3306
CMD ["/run.sh"]
