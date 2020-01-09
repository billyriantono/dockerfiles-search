# Cookhouse
# Docker-based development environment
FROM archlinux/base
MAINTAINER "admin@radix10.cn"


# Username
ARG USERNAME=cook
# Vimrc file
ARG VIMRC=/home/$USERNAME/.config/nvim/init.vim


# Install package
RUN pacman -Syu --noconfirm && pacman -S --noconfirm --needed sudo git git-lfs \
    neovim python-neovim go nodejs npm jq rsync

# Create user
RUN useradd -m -g users -G wheel -s /bin/bash $USERNAME && passwd -d $USERNAME \
    && sed -i 's/^# %wheel ALL=(ALL) ALL$/%wheel ALL=(ALL) ALL/g' /etc/sudoers


# Switch user
USER $USERNAME


# Config neovim
# Install vim-plug
RUN curl -fLso ~/.local/share/nvim/site/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

# Copy init.vim
COPY --chown=cook:users .config/nvim/init.vim $VIMRC

# Install vim plugin
RUN nvim --headless +PlugInstall +qall

#Enable theme
RUN sed -i 's/^"colorscheme NeoSolarized/colorscheme NeoSolarized/g' $VIMRC

WORKDIR /home/$USERNAME
