FROM alvrme/alpine-android-base
LABEL maintainer="Tom Lloyd <thomaslloyd@yahoo.com>"


ENV KEYSTORE_FILE=keystore
ENV KEYSTORE_PASSWORD=AndroidAPS
ENV KEYSTORE_ALIAS=key0
ENV VERSION=master

VOLUME [ "/home/aaps" ]
WORKDIR /home/aaps
COPY build-aaps /usr/bin
RUN chmod +x /usr/bin/build-aaps

# Install a local webserver and link to the APK output
# folder so users can navigate and install APKs directly
# from their phones after the build process is finished.
RUN apk add -U --no-cache apache2
RUN rm -rf /var/www/localhost/htdocs
RUN ln -s -f /home/aaps/ /var/www/localhost/htdocs
RUN sed -i 's/Listen 80/Listen 8080/g' /etc/apache2/httpd.conf

EXPOSE 80/tcp
CMD build-aaps
