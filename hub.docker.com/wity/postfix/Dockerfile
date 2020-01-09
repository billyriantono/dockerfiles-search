FROM opensuse/leap

# I think we don't need to maintain content of /var/log and /var/cache.
# If you ever want to do that, do it before the following VOLUME command.
VOLUME [ "/var/log", "/var/cache" ]

# Postfix's start script needs /usr/bin/hostname.
# You might need busybox for syslogd replacement.
RUN zypper in --no-recommends -y postfix hostname busybox && zypper clean -a

COPY ./start-postfix /
ENTRYPOINT [ "/start-postfix" ]

EXPOSE 25 465 587
