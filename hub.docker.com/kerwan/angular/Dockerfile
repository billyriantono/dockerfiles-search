FROM node:10-stretch

#<<<
# INSTALL ANGULAR CLI
#<<<
RUN npm install -g @angular/cli

#<<<
# SETTING UP ENTRYPOINT
#<<<
COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["--host=0.0.0.0"]