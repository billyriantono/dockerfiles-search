# Minimal setup that is needed to run Haskell binaries
# build with GHC-7.8 on ubuntu trustyt.
#
# It's not really minimal and not all binaries are supported.
# I add more dependencies as needed.

FROM scratch
MAINTAINER Lars Kuhtz <larskuhtz@kuhtz.eu>

ADD tmp /tmp
ADD var /var
ADD etc /etc
ADD bin /bin
ADD lib64/ /lib64
ADD lib /lib
ADD usr/ usr

RUN /bin/busybox chown -R 0.0 /bin /tmp /var /etc /lib /lib64 /usr

