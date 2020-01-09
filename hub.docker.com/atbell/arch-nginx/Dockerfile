FROM atbell/arch-base
MAINTAINER atbell

# install application
#####################

# update package databases for arch
RUN pacman -Sy --noconfirm

# run packer to install application
RUN pacman -S nginx --noconfirm

# map /config to host defined config path (used to store configuration from app)
VOLUME /config

# map /data to host defined data path (used to store data from app [logs, etc])
VOLUME /data

# expose port for http
EXPOSE 80

# expose port for https
EXPOSE 443

# copy prerun bash shell script (checks for existence of nginx config)
ADD prerun.sh /etc/supervisor/conf.d/prerun.sh

# make prerun bash shell script executable
RUN chmod +x /etc/supervisor/conf.d/prerun.sh

# set permissions
#################

# change owner
RUN chown -R nobody:users /usr/sbin/nginx

# set permissions
RUN chmod -R 775 /usr/sbin/nginx

# add conf file
###############

ADD nginx.conf /etc/supervisor/conf.d/nginx.conf

# cleanup
#########

# completely empty pacman cache folder
RUN pacman -Scc --noconfirm

# remove temporary files
RUN rm -rf /tmp/*

# run supervisor
CMD ["supervisord", "-c", "/etc/supervisor.conf", "-n"]
