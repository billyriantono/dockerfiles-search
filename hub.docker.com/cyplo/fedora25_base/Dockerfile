FROM fedora:25

RUN dnf -y install sudo
RUN sudo dnf -y upgrade --best --allowerasing
RUN sudo dnf -y --best --allowerasing install tmux atop zsh thunderbird thunderbird-enigmail thunderbird-lightning firefox aria2 gajim lm_sensors freecad python3-pip qt5-qtbase-devel qt5-qtwebkit-devel meld whois curl pv nodejs npm terminator gsmartcontrol python-pip mercurial python3-devel libxslt-devel libjpeg-turbo-devel conky conky-manager redshift redshift-gtk cmake gtk2-devel intltool gparted wine solaar glances the_silver_searcher dkms kernel-devel gimp transmission-gtk git xz util-linux-user powertop dnf-automatic kdiff3 yum-utils util-linux-user ncurses-devel zeal qt5-linguist qtkeychain-qt5-devel archivemount keepass splix gutenprint-cups cups-bjnp golang redhat-rpm-config docker pcsc-lite-devel pcsc-tools pcsc-lite yubico-piv-tool yubikey-personalization-gui xloadimage yp-tools closure-compiler optipng jpegoptim

RUN sudo dnf -y groupinstall "C Development Tools and Libraries"
RUN sudo dnf -y groupinstall "Development Tools"

# vscode
RUN sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
RUN sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
RUN sudo dnf -y install --best --allowerasing code

# dotnet
RUN sudo dnf -y copr enable nmilosev/dotnet-sig
RUN sudo dnf -y install dotnetcore

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

RUN git clone https://github.com/rust-lang/rust.git --recursive /root/dev/rust

RUN curl -sSf https://sh.rustup.rs > /tmp/rustup
RUN chmod a+x /tmp/rustup
RUN /tmp/rustup -y
RUN rm -f /tmp/rustup
RUN /root/.cargo/bin/rustup update
RUN /root/.cargo/bin/rustup default stable  
RUN /root/.cargo/bin/cargo install rustfmt
RUN /root/.cargo/bin/cargo install racer
RUN /root/.cargo/bin/cargo install rustsym
RUN /root/.cargo/bin/cargo install ripgrep
RUN /root/.cargo/bin/cargo install just
RUN /root/.cargo/bin/cargo install cargo-update

