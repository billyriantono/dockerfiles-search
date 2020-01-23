FROM eluminae/archlinux-aurman

RUN sudo -u aur aurman -S --noconfirm --noedit imapfilter && \
    yes | pacman -Scc && \
    rm -rf /home/aur/.cache/aurman

RUN useradd -m imapfilter && \
	passwd -d imapfilter && \
	sudo -u imapfilter mkdir -p /home/imapfilter/.imapfilter

WORKDIR /home/imapfilter
USER imapfilter
CMD ["imapfilter"]
