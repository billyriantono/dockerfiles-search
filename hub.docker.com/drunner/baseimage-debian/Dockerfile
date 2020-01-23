# Simple baseimage for dServices using Debian.

FROM debian
MAINTAINER j842

# we use non-root user in the container for security.
RUN groupadd -g 22021 drgroup
RUN adduser --disabled-password --gecos '' -u 22021 --gid 22021 druser

# create /drunner and allow druser write access.
RUN mkdir /drunner && chown druser:drgroup /drunner

# derived containers need to switch to the non-root user:
# USER druser
