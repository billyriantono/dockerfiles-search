FROM mongo:3.6

MAINTAINER <John S. Lutz> jlutz@broadiq.com

ENV AUTH yes

ENV MONGODB_ADMIN_USER root 
# ENV MONGODB_ADMIN_PASS password

# ENV MONGODB_APPLICATION_DATABASE your_db
# ENV MONGODB_APPLICATION_USER user
# ENV MONGODB_APPLICATION_PASS password

EXPOSE 27017 27017

ADD run-config.sh /run-config.sh
ADD set-password.sh /set-password.sh

RUN chmod +x /run-config.sh
RUN chmod +x /set-password.sh

CMD ["/run-config.sh"]
