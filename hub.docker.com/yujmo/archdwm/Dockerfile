FROM yujmo/archbase:latest
RUN yaourt -S xorg-server --noconfirm && yaourt -S xorg-server-xvfb --noconfirm \
	&& yaourt -S make --noconfirm \
	&& yaourt -S xterm --noconfirm \
	&& yaourt -S dwm --noconfirm \
	&& yaourt -R dwm --noconfirm \
	&& yaourt -S gcc --noconfirm
ADD dwm /dwm
RUN cd /dwm && make && make install && yaourt -S fcitx --noconfirm \
	&& yaourt -S supervisor --noconfirm \
	&& yaourt -S x11vnc --noconfirm 
ADD xinitrc.mo /tmp/xinitrc
RUN rm -rf /root/.xinitrc && mv /tmp/xinitrc /root/.xinitrc
