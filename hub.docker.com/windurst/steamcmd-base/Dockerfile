FROM windurst/docker-glibc:2.18
ENV RUNUSER daemon
ENV DAEMON_HOME /home/${RUNUSER}
ENV STEAMCMD_LOC ${DAEMON_HOME}/steamcmd
ENV STEAMCMD ${STEAMCMD_LOC}/steamcmd.sh
RUN yum update -y
RUN yum install curl -y
RUN yum install glibc.i686 libstdc++.i686 -y
RUN mkdir -p ${STEAMCMD_LOC}  && \
        curl -s http://media.steampowered.com/installer/steamcmd_linux.tar.gz | tar -v -C ${STEAMCMD_LOC} -zx && \
        chown -R ${RUNUSER}:${RUNUSER} ${DAEMON_HOME}

WORKDIR ${STEAMCMD_LOC}

USER ${RUNUSER}
RUN ${STEAMCMD} +login anonymous validate +quit
ENTRYPOINT ["/home/daemon/steamcmd/steamcmd.sh"]
