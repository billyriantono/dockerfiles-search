FROM base/archlinux

RUN pacman -Syyu --needed --noconfirm \
	python2 \
	&& rm -f /var/cache/pacman/pkg/*.tar.xz

CMD ["python2"]