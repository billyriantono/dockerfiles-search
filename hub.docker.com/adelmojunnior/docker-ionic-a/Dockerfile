FROM adbv/base

LABEL maintainer="Günther Morhart"

#
# Environment variables
#

#
# Setup
#
RUN apk add --no-cache \
        vsftpd

RUN { \
        echo 'listen=YES'; \
        echo 'local_enable=YES'; \
        echo 'xferlog_enable=YES'; \
        echo 'connect_from_port_20=YES'; \
        echo 'pam_service_name=vsftp'; \
        echo 'seccomp_sandbox=NO'; \
        # enable upload by local user
        echo 'write_enable=YES'; \
        # Enable read by anonymous user (without username and password).
        echo 'secure_chroot_dir=/var/empty'; \
        echo 'anonymous_enable=YES'; \
        echo 'anon_root=/srv/ftp'; \
        echo 'no_anon_password=YES'; \
        echo 'anon_upload_enable=YES'; \
        echo 'anon_other_write_enable=YES'; \
        echo 'anon_mkdir_write_enable=YES'; \
        echo 'anon_world_readable_only=NO'; \
        echo 'pasv_promiscuous=YES'; \
    } > /etc/vsftpd/vsftpd.conf && \
    mkdir /srv/ftp && \
    chown nobody:nogroup /srv/ftp



#
# Command
#
EXPOSE 21

CMD ["vsftpd", "/etc/vsftpd/vsftpd.conf"]