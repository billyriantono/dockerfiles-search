FROM ubuntu
ENV DEBIAN_FRONTEND noninteractive
RUN apt update && apt upgrade -y && apt install -y make gcc git curl \
    boxes sl cowsay fortune-mod lolcat nyancat cmatrix toilet figlet linuxlogo aview espeak rig bastet ninvaders pacman4console nsnake greed moon-buggy hollywood libaa-bin bb fortune-zh crawl gearhead omega-rpg tome zangband bsdgames-nonfree nudoku emacs-nox bastet

WORKDIR /root
# 安装tetris
RUN curl -L https://github.com/samtay/tetris/releases/download/0.1.2/tetris-`uname -s`-`uname -m` -o /usr/bin/tetris && chmod +x /usr/bin/tetris
# 安装2048-cli
RUN git clone https://github.com/tiehuis/2048-cli.git && cd 2048-cli && make && mv 2048 /usr/bin && cd /root && rm -rf 2048-cli

# 安装snake-game
# RUN go gettgithub.com/DyegoCosta/snake-game && mv $GOPATH/bin/snake-game /usr/bin/snake-game
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games

# 安装pony-say
RUN curl http://www.vcheng.org/ponysay/ponysay_3.0.2-1_all.deb -o ponysay.deb && \
        dpkg -i ponysay.deb && \
        rm -f ponysay.deb