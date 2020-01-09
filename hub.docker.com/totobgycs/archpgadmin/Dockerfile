FROM totobgycs/archdevx11
MAINTAINER totobgycs

ENV TERM xterm
RUN yaourt -Syy ; \
   yaourt -S --aur --noconfirm pgadmin4 ; \
   yes | yaourt -Scc

WORKDIR /home/guiuser
USER guiuser
#ENTRYPOINT ["pgadmin4"]
