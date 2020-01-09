FROM pritunl/archlinux
RUN pacman -S --noconfirm python-jinja
COPY render.py /usr/local/bin/render.py
COPY fork_proxy.sh /usr/sbin/fork_proxy.sh

