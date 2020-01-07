FROM mikiyamizui/alpine

RUN apk update \
    && apk add --no-cache sudo less git vim fish

RUN sed -i -e 's;root:/bin/ash$;root:/sbin/nologin;g' /etc/passwd \
    && addgroup -g 1000 -S dev \
    && adduser -u 1000 -G dev -s $(which fish) -D -S dev \
    && echo "dev ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/dev \
    && chmod 0440 /etc/sudoers.d/dev \
    && sed -i -e "s;/bin/ash;$(which fish);g" /etc/passwd

USER dev
SHELL [ "/usr/bin/fish", "-c" ]
COPY --chown=dev:dev ./dotfiles /home/dev
RUN curl https://git.io/fisher --create-dirs -sLo ~/.config/fish/functions/fisher.fish \
    && fisher add \
    fishpkg/fish-git-util \
    joseluisq/gitnow@2.1.1 \
    rafaelrinaldi/pure

ENV USER dev
ENV HOME /home/dev
