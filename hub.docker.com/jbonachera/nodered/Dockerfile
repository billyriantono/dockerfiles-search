FROM jbonachera/arch
ENTRYPOINT ["/sbin/entrypoint.sh"]
VOLUME /var/lib/nodered
RUN useradd -r nodered -d /var/lib/nodered
RUN pacman  -S --noconfirm npm 
RUN npm install -g node-red
WORKDIR /var/lib/nodered
COPY entrypoint.sh /sbin/entrypoint.sh
