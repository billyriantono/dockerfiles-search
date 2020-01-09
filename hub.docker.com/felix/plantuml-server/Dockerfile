FROM jetty:alpine

USER root
RUN apk add --no-cache graphviz fontconfig ttf-dejavu

# http://plantuml.com/download
ADD ./plantuml.war /var/lib/jetty/webapps/plantuml.war
USER jetty

EXPOSE 8080

