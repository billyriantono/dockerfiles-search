#Dockerfile

FROM anapsix/alpine-java
RUN mkdir /cbs
WORKDIR /cbs
RUN mkdir /cbs/cachebox 
COPY cbs/ /cbs/
VOLUME /cbs/cachebox

EXPOSE 8085
EXPOSE 9911
CMD java -jar cbserver.jar -Xmx2048m
