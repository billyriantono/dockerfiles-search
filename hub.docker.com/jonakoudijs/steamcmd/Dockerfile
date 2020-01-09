######## BUILDER ########

# Set the base image to Ubuntu SteamCMD
# hadolint ignore=DL3007
FROM jonakoudijs/steamcmd:latest as builder

# Update SteamCMD
RUN steamcmd +quit

######## INSTALL ########

# Set the base image to Ubuntu
FROM busybox:1.30

# Set environment variables
ENV LD_LIBRARY_PATH /usr/sbin

# Copy steamcmd and required files from builder
COPY --from=builder /root/.steam/steamcmd/linux32 /usr/sbin
COPY --from=builder /etc/ssl/certs /etc/ssl/certs
COPY --from=builder /lib/i386-linux-gnu /lib/
COPY --from=builder /lib/ld-linux.so.2  /lib/

# Cache bust forcing SteamCMD update
ADD https://www.random.org/cgi-bin/randbyte?nbytes=32&format=h $HOME/.cachebust

# Update SteamCMD
# hadolint ignore=SC2216,DL4006
RUN steamcmd +quit | true

# Set default command
CMD ["steamcmd", "+help", "+quit"]
