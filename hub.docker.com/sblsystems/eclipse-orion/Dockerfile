FROM java:8

ENV ORION_HOST=localhost

RUN curl -o /tmp/orion.zip http://ftp-stud.fht-esslingen.de/pub/Mirrors/eclipse/orion/drops/R-11.0-201602232219/eclipse-orion-11.0-linux.gtk.x86_64.zip && \
    cd /opt && unzip /tmp/orion.zip && \
    rm -rf /tmp/orion.zip

RUN chmod +x /opt/eclipse/orion

RUN echo $ORION_HOST > /opt/eclipse/env.txt

EXPOSE 8080

WORKDIR /opt/eclipse

ADD  orion.conf /opt/eclipse/orion.conf
ADD  .gitconfig /root/.gitconfig

CMD ["/opt/eclipse/orion"]