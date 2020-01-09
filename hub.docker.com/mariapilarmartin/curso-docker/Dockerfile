FROM nginx:1.15

ENV DIRCONF /etc/nginx/conf.d/
ENV DIRSTATICS /opt/project

RUN mkdir -p $DIRSTATICS

COPY default.conf $DIRCONF/default.conf

#COPY index.html  => preguntar si es necesario

#EXPOSE 90/tcp

VOLUME $DIRSTATICS

ENTRYPOINT ["nginx"] 
CMD ["-g", "daemon off;"]
 
 
 
 
 
 FROM nginx:1.15
ENV DIR /opt/project
RUN mkdir -p $DIR
COPY default.conf /etc/nginx/conf.d/default.conf
WORKDIR $DIR
COPY index.html .
EXPOSE 90/tcp
VOLUME $DIR 
CMD ["nginx", "-g", "daemon off;"]
