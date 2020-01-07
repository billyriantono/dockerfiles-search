FROM patricol/gui_base:arch

#If the program doesn't work, clear its config files, and potentially run without -s.

RUN update \
 && addpackages \
    google-musicmanager \
    log4cxx \
 && clearcache \
 && ln -sf /config/ ~/.config/google-musicmanager \
 && echo "sudo chown user:users /config" >> /scripts/startapp \
 && echo "exec google-musicmanager -s /music" >> /scripts/startapp

VOLUME /config
VOLUME /music
