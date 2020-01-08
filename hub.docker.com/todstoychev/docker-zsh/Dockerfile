FROM ubuntu:18.04
RUN apt-get update && apt-get install zsh curl vim wget git fontconfig language-pack-en -y
RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
RUN git clone https://github.com/bhilburn/powerlevel9k.git ~/.oh-my-zsh/custom/themes/powerlevel9k

RUN wget https://github.com/powerline/powerline/raw/develop/font/PowerlineSymbols.otf && \
wget https://github.com/powerline/powerline/raw/develop/font/10-powerline-symbols.conf && \
mkdir -p /root/.local/share/fonts/ && \
mv PowerlineSymbols.otf ~/.local/share/fonts/ && \
fc-cache -vf ~/.local/share/fonts/ && \
mkdir -p ~/.config/fontconfig/conf.d/ && \
mv 10-powerline-symbols.conf ~/.config/fontconfig/conf.d/

COPY ./zshrc /root/.zshrc

ENTRYPOINT ["zsh"]
