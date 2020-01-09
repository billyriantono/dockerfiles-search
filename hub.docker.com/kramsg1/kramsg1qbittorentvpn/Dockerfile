FROM binhex/arch-int-openvpn:latest
MAINTAINER speed1405 & kramsg12



# additional files
##################

# add supervisor conf file for app
ADD build/*.conf /etc/supervisor/conf.d/

# add bash scripts to install app
ADD build/root/*.sh /root/

# add run bash scripts
ADD run/root/*.sh /root/

# add run bash scripts
ADD run/nobody/*.sh /home/nobody/

# add pre-configured config files for nobody
ADD config/nobody/ /home/nobody/

# install app
#############

# make executable and run bash scripts to install app
RUN chmod +x /root/*.sh /home/nobody/*.sh && \
	/bin/bash /root/install.sh

# docker settings
#################

# map /config to host defined config path (used to store configuration from app)
VOLUME /config

# map /data to host defined data path (used to store data from app)
VOLUME /data

COPY ca.rsa.2048.crt ~/home/openvpn
COPY ca.rsa.2048.crt.1 ~/home/openvpn
COPY CA_Vancouver.ovpn ~/home/openvpn
COPY crl.rsa.2048.pem ~/home/openvpn
COPY Denmark.ovpn ~/home/openvpn


# expose port for incoming connections (used only if vpn disabled)
EXPOSE 6881

# expose port for qbittorrent http
EXPOSE 8080

# expose port for privoxy
EXPOSE 8118

# set permissions
#################

# run script to set uid, gid and permissions
CMD ["/bin/bash", "/root/init.sh"]
