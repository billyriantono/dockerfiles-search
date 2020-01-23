# Use an official Python runtime as a parent image
FROM alpine:latest

# Initial installation
RUN apk update \
&& apk upgrade \
&& apk add util-linux htop tree vim git curl groff bc ncurses fish \
&& rm -rf /var/cache/apk/* \
&& curl -L https://get.oh-my.fish > ~/omf.fish \
&& fish ~/omf.fish --noninteractive --path=~/.local/share/omf --config=~/.config/omf \
&& echo 'omf install budspencer;fish_update_completions;set -U budspencer_nogreeting;rm ~/omf.fish;rm ~/.config/fish/config.fish' > ~/.config/fish/config.fish \
&& fish

ENTRYPOINT ["fish"]
