FROM java:8
RUN apt-get update && apt-get install -y \
    nano \
    joe
CMD ["mkdir", "-p","/home/app/"]
COPY Files/app/TestGCloud-0.1.0.jar /home/app/
CMD ["mkdir", "-p", "/config/"]
COPY Files/config/* /config/
EXPOSE 9092
COPY docker-entrypoint.sh /
RUN  chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]


