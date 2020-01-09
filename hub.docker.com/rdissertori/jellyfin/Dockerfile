FROM jellyfin/jellyfin:latest
ENV UID=1000
VOLUME ["/config","/media","/cache"]
RUN useradd -u ${UID} jellyfin -G users \
&& groupadd -g 107 render \
&& gpasswd -a jellyfin video \
&& gpasswd -a jellyfin render \
&& chown jellyfin:users -R /config /media /cache
USER jellyfin
