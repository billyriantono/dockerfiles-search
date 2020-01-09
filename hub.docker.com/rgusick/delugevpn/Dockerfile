FROM    binhex/arch-delugevpn

MAINTAINER Robert Gusick "robert@gusick.com"

RUN     pacman -S --needed --noconfirm \
        ssmtp \
        s-nail
        
RUN     touch /var/spool/mail/root
