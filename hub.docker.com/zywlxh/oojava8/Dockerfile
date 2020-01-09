FROM java:8


RUN mkdir /openoffice

COPY ./zh-CN /openoffice

RUN chmod u+x -R /openoffice \
   && dpkg -i /openoffice/DEBS/*.deb \
   && echo "install desktop service ..." \
   && dpkg -i /openoffice/DEBS/desktop-integration/openoffice4.1-debian-menus_4.1.6-9790_all.deb \
   && echo "install finshed..." && rm -rf /openoffice

#RUN dpkg -i /openoffice/DEBS/*.deb
#RUN echo "install desktop service ..."
#RUN dpkg -i /openoffice/DEBS/desktop-integration/openoffice4.1-debian-menus_4.1.6-9790_all.deb
#RUN echo "install finshed..."
