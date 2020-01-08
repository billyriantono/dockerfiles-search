FROM alpine:3.8
LABEL authors="Serge NOEL <serge.noel@net6a.com>"

# Files contain all the preconfigured files launch 'tree' command to see what is included 
ADD Files/ /
# Create Conf folders
# As we will use /AD to store samba specific files, we need to link those files to be able to do a 'ln' linux command against
# When the container will be initiated, initial script will make necessary job
RUN mkdir -p /AD/etc /AD/etc/samba /AD/etc/cups /AD/etc/sssd /AD/var/lib/samba /AD/var/lib/samba/private /AD/var/log/samba /AD/Data \
    && touch /AD/var/lib/samba/private/krb5.conf \
    && ln -s /AD/etc/samba /etc/samba \
    && ln -s /AD/var/lib/samba /var/lib/samba \
    && ln -s /AD/var/log/samba /var/log/samba \
    && ln -s /AD/Data /Data \
    && ln -s /AD/var/lib/samba/private/krb5.conf /etc/krb5.conf \
    && apk update \
    && apk add samba-dc samba-client bind supervisor tdb \
    && rm /etc/samba/smb.conf \
    && chmod a+x /usr/local/bin/launch-samba \
    && chmod a+x /usr/local/bin/setup-samba \
    && rm -rf /var/cache/apk/*

# apk add samba-dc samba-client bind bind-tools supervisor krb5-server tdb rsyslog

# Install samba
EXPOSE 53 389 88 135 139 138 445 464 3268 3269 123/udp

VOLUME /AD

CMD ["/usr/local/bin/launch-samba"]

