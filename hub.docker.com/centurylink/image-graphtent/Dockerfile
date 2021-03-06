## Refer to the GitHub repository for configuration and problems.
## Cenk Kilic <cenk@kilic.dev>
## https://srcs.kilic.dev/softether-vpncli

FROM alpine:latest

RUN apk --no-cache --no-progress update && \
    apk --no-cache --no-progress upgrade && \
    # Install s6 supervisor
    apk --no-cache --no-progress add s6 bash && \
    mkdir /s6 && mkdir /s6-bin && mkdir /s6/.s6-svscan && \
    # Install build dependencies
    apk --no-cache --no-progress --virtual .build-deps add git libgcc libstdc++ gcc musl-dev libc-dev g++ ncurses-dev \
    readline-dev openssl-dev cmake make zlib-dev && \
    # Grab and build Softether from GitHub
    git clone https://github.com/SoftEtherVPN/SoftEtherVPN.git /tmp/softether && \
    cd /tmp/softether && git submodule init && git submodule update && export USE_MUSL=YES && \
    ./configure && make --silent -C tmp && make --silent -C tmp install &&  \
    cp /tmp/softether/build/libcedar.so /tmp/softether/build/libmayaqua.so /usr/lib && \
    # Removing build extensions
    apk del .build-deps && apk del --no-cache --purge && \
    rm -rf /tmp/softether && rm -rf /var/cache/apk/* && \
    # Deleting unncessary extensions
    rm -rf /usr/local/bin/vpnbridge /usr/local/bin/vpnserver \
    /usr/local/libexec/softether/vpnbridge /usr/local/libexec/softether/vpnserver && \
    # Reintroduce necassary libraries
    apk add --no-cache --virtual .run-deps \
    libcap libcrypto1.1 libssl1.1 ncurses-libs readline su-exec dhclient && \
    # Link Libraries to Binary
    mkdir /s6-bin/softether-vpncli && \
    ln -s /usr/local/bin/vpnclient /s6-bin/softether-vpncli/vpnclient && \
    ln -s /usr/local/bin/vpncmd /s6-bin/softether-vpncli/vpncmd && \
    # Link the connection profile as well since there is a bug with importing from directory
    apk add --no-cache expect && \
    # Install SAMBA Daemon
    apk --no-cache --no-progress add samba && \
    # Create SAMBA User
    adduser -D -G users -H -S -g 'Samba User' -h /tmp smbuser && \
    # Initiate Samba Configuration File
    file="/etc/samba/smb.conf" && \
    sed -i 's|^;* *\(log file = \).*|   \1/dev/stdout|' $file && \
    sed -i 's|^;* *\(load printers = \).*|   \1no|' $file && \
    sed -i 's|^;* *\(printcap name = \).*|   \1/dev/null|' $file && \
    sed -i 's|^;* *\(printing = \).*|   \1bsd|' $file && \
    sed -i 's|^;* *\(unix password sync = \).*|   \1no|' $file && \
    sed -i 's|^;* *\(preserve case = \).*|   \1yes|' $file && \
    sed -i 's|^;* *\(short preserve case = \).*|   \1yes|' $file && \
    sed -i 's|^;* *\(default case = \).*|   \1lower|' $file && \
    sed -i '/Share Definitions/,$d' $file && \
    echo '   pam password change = yes' >>$file && \
    echo '   map to guest = bad user' >>$file && \
    echo '   usershare allow guests = yes' >>$file && \
    echo '   create mask = 0664' >>$file && \
    echo '   force create mode = 0664' >>$file && \
    echo '   directory mask = 0775' >>$file && \
    echo '   force directory mode = 0775' >>$file && \
    echo '   force user = smbuser' >>$file && \
    echo '   force group = users' >>$file && \
    echo '   follow symlinks = yes' >>$file && \
    echo '   load printers = no' >>$file && \
    echo '   printing = bsd' >>$file && \
    echo '   printcap name = /dev/null' >>$file && \
    echo '   disable spoolss = yes' >>$file && \
    echo '   socket options = TCP_NODELAY' >>$file && \
    echo '   strict locking = no' >>$file && \
    echo '   vfs objects = acl_xattr catia fruit recycle streams_xattr' \
                >>$file && \
    echo '   recycle:keeptree = yes' >>$file && \
    echo '   recycle:versions = yes' >>$file && \
    echo '' >>$file && \
    echo '   # Security' >>$file && \
    echo '   client ipc max protocol = default' >>$file && \
    echo '   client max protocol = default' >>$file && \
    echo '   server max protocol = SMB3' >>$file && \
    echo '   client ipc min protocol = default' >>$file && \
    echo '   client min protocol = CORE' >>$file && \
    echo '   server min protocol = SMB2' >>$file && \
    echo '' >>$file && \
    echo '   # Time Machine' >>$file && \
    echo '   durable handles = yes' >>$file && \
    echo '   kernel oplocks = no' >>$file && \
    echo '   kernel share modes = no' >>$file && \
    echo '   posix locking = no' >>$file && \
    echo '   fruit:aapl = yes' >>$file && \
    echo '   fruit:advertise_fullsync = true' >>$file && \
    echo '   fruit:time machine = yes' >>$file && \
    echo '   smb2 leases = yes' >>$file && \
    echo '' >>$file && \
    # Clean Up Files
    rm -rf /tmp/*

# Move s6 supervisor files inside the container
ADD ./s6 /s6
# Move Binaries to bin
ADD ./s6-bin /s6-bin

# Expose samba ports
EXPOSE 139 445

ENTRYPOINT [ "/bin/s6-svscan", "/s6" ]
