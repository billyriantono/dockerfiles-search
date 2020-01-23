FROM archlinux/base

RUN pacman -Syu --noconfirm

RUN pacman -S wget awk grep filesystem cmake make vim gcc kdelibs4support git  xorg-server libglvnd libx11 root --noconfirm

WORKDIR /root/

RUN	wget https://plutouser.github.io/v6.01/pluto_v6.01.tar.gz \
	&& tar xvf pluto_v6.01.tar.gz \
	&& rm pluto_v6.01.tar.gz \
	&& mkdir pluto_v6.01/build \
	&& cd /root/pluto_v6.01/build \
	&& cmake ../ . \
	&& make -j4 \
	&& cd /root/ 

RUN echo "echo ""; echo "Welcome in pluto-GSI container [https://github.com/aszadzinski/dockerfiles/tree/master/physics-simulations/pluto-GSI]"; echo "You can find libPluto.so in pluto_v6.01/build/"; echo ""; echo "Type:"; echo "  sh init.sh"; echo "to execute Public/run.sh."; echo "" " >> .bashrc
RUN echo "echo "Opening Public/run.sh file..."; echo ""; sh /root/Public/run.sh; echo ""; echo "Done."" >> init.sh 

#ENTRYPOINT ["sh","init.sh"]
CMD sh init.sh
