FROM 4577/soko-onbuild
MAINTAINER Tristan GRUNERT tristan.grunert@epitech.eu

ENV TERM xterm

COPY src/ /home/src/
COPY lvl.sh /home/
COPY map_folder/ /home/map_folder/
COPY gg.asciiart /home/
WORKDIR /home/src/
RUN make -s ; make -s clean
RUN rm -rf /home/src/

#CMD ["/home/my_sokoban", "/home/src/map_folder/map.txt"]
WORKDIR /home/
CMD /home/lvl.sh