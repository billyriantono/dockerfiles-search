FROM fdiblen/archsci:latest
MAINTAINER fdiblen

USER root

# INSTALL EXTRA PACKAGES
# ===================================
RUN pacman -Syyu --noconfirm --needed \
    npm python2-pandas python2-sqlalchemy python2-psycopg2 lighttpd


# ADD SCRIPTS
RUN mkdir -p /home/archsci/temp
ADD scripts/set/*.sh /home/archsci/temp/
ADD scripts/serve/*.sh /usr/local/bin/
RUN chmod +x  /home/archsci/temp/*.sh /usr/local/bin/*.sh


# SETUP - WEB SERVER
# ===================================
ADD confs/lighttpd.conf /home/archsci/web/lighttpd.conf
RUN /home/archsci/temp/set_web.sh


# SETUP - SPOT
# ===================================
USER archsci
ENV DISPLAY :0
ENV EDITOR vim
RUN /home/archsci/temp/set_spot.sh


# SETUP - DATABASE SERVER
# ===================================
USER root
RUN /home/archsci/temp/set_postgres.sh


# ADJUST PERMISSIONS and CLEAN UP
# ===================================
USER root
ENV DISPLAY :0
ENV EDITOR vim
RUN chown -R archsci:archsci /home/archsci/ && \
    rm -rf /home/archsci/temp


# SERVE
# ===================================
USER archsci
ENV DISPLAY :0
ENV EDITOR vim

EXPOSE 3080 5432 80 443

CMD ["/usr/local/bin/serveAll.sh"]
