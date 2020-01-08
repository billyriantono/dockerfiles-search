FROM archlinux/base
EXPOSE 8303/udp

WORKDIR /var/teeworlds
RUN pacman -Syu --noconfirm --needed teeworlds

RUN mkdir data_home 
ENV XDG_DATA_HOME=/var/teeworlds/data_home

COPY conf/server.cfg conf/server.cfg

ENV TEEWORLDS_PASSWORD=""
CMD if [ "$TEEWORLDS_PASSWORD" != "" ]; then sed -i "s/^sv_rcon_password .*$/sv_rcon_password $TEEWORLDS_PASSWORD/g" conf/server.cfg; fi && \
    teeworlds_srv -f conf/server.cfg
