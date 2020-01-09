FROM fedora:28

RUN dnf -y install sudo
RUN sudo dnf -y upgrade --best --allowerasing
RUN sudo dnf -y --best --allowerasing install tmux atop zsh firefox aria2 gajim lm_sensors freecad python3-pip qt5-qtbase-devel qt5-qtwebkit-devel meld whois curl pv nodejs npm terminator gsmartcontrol python-pip mercurial python3-devel libxslt-devel libjpeg-turbo-devel conky conky-manager cmake gtk2-devel intltool gparted wine solaar glances the_silver_searcher dkms kernel-devel gimp transmission-gtk git xz util-linux-user powertop dnf-automatic kdiff3 yum-utils util-linux-user ncurses-devel zeal qt5-linguist qtkeychain-qt5-devel archivemount keepass splix gutenprint-cups cups-bjnp golang redhat-rpm-config pcsc-lite-devel pcsc-tools pcsc-lite yubico-piv-tool yubikey-personalization-gui xloadimage yp-tools closure-compiler optipng jpegoptim grub2 grub2-efi dracut dracut-tools openssl-devel fail2ban syncthing ansible

RUN sudo dnf -y groupinstall "C Development Tools and Libraries"
RUN sudo dnf -y groupinstall "Development Tools"

RUN mkdir -p /root/dev/
# vim
RUN git clone https://github.com/vim/vim.git --recursive /root/dev/vim
RUN cd /root/dev/vim && ./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp \
            --enable-python3interp=yes \
            --enable-luainterp \
            --enable-gui=no \
            --enable-cscope 
RUN cd /root/dev/vim && make -j`nproc`
RUN cd /root/dev/vim && sudo make install

