FROM talm0/texlive

RUN add-apt-repository -y ppa:libreoffice/libreoffice-6-0
RUN apt update && apt install -y gcc make m4 zip qpdf mercurial git inkscape python-pygments libreoffice iproute2

# Bionic no longer supports APT installation of pdftk
# We'll do it manually
COPY install-pdftk /tmp
RUN bash /tmp/install-pdftk && rm /tmp/install-pdftk

COPY host-dns-chain.sh /etc/my_init.d/00-host-dns.sh
RUN chmod +x /etc/my_init.d/00-host-dns.sh

ENTRYPOINT ["/bin/bash", "/etc/my_init.d/00-host-dns.sh"]
