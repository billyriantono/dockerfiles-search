FROM fedora:latest
RUN dnf install curl unzip -y
RUN curl -o /tmp/openarena.zip http://download.tuxfamily.org/openarena/rel/088/openarena-0.8.8.zip

RUN mkdir -p /opt/openarena
### We are going to mount this for our server.cfg
# -v /opt/openarena /root/.openarena/baseoa
RUN mkdir -p /root/.openarena/baseoa
RUN cd /tmp && unzip /tmp/openarena.zip -d /opt/openarena && rm openarena.zip
RUN rm -rf /tmp/* /var/tmp/*
## I will remove this later and expose a mount
#ADD server.cfg /opt/openarena/openarena-0.8.8/baseoa/


EXPOSE 27960/udp
EXPOSE 27950/udp

#Run my_init
CMD /opt/openarena/openarena-0.8.8/oa_ded.x86_64 +set dedicated 1 +set sv_cheats 1 +exec server.cfg
