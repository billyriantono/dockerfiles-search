FROM alpine
MAINTAINER Patrick Farrell <patrick@creativecollisionstech.com>

# Install samba
RUN apk --no-cache --no-progress upgrade && \
    apk --no-cache --no-progress add bash samba shadow tini && \
    adduser -D -G users -H -S -g 'Samba User' -h /tmp smbuser   # If you remove this line, doesn't work, not sure why