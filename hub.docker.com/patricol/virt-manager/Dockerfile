FROM patricol/gui_base:arch

RUN update \
 && addpackages \
    virt-manager \
 && clearcache \
 && ln -sf /config/ ~/.config/dconf \
 && echo "sudo chown user:users /config" >> /scripts/startapp \
 && echo "exec virt-manager" >> /scripts/startapp

VOLUME /config
