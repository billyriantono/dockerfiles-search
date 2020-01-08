FROM base/archlinux:latest
RUN pacman -Syu 
RUN pacman -S --noconfirm git base-devel netcat tar
RUN useradd -m makerman
RUN echo "makerman ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/makerman
USER makerman
WORKDIR /home/makerman
RUN git clone https://aur.archlinux.org/minecraft-server.git
WORKDIR /home/makerman/minecraft-server
RUN makepkg -si --noconfirm
USER minecraft
WORKDIR /srv/minecraft
RUN echo "eula=true" >> /srv/minecraft/eula.txt
USER root
RUN systemctl enable minecraftd
CMD [“/usr/sbin/init”]
