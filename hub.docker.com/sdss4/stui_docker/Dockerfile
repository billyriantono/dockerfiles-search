# sdss/stui_docker

FROM ubuntu:15.10
MAINTAINER Joel Brownstein <joelbrownstein@astro.utah.edu>
LABEL build="Ubuntu 15.10 with python (June 13, 2015 2:28:00MDT)"

# ========================================================
# USERS > stui_user
# ========================================================

RUN apt-get update \
    && apt-get install -y vim sudo rsyslog subversion git lmod tclsh openssh-server \
	&& rm -rf /var/lib/apt/lists/*

RUN mkdir -p /tmp/bin
ADD users/stui_user/tmp/bin /tmp/bin/
RUN chmod +rx /tmp/bin/*
RUN mkdir -p /var/run/sshd && sed -i "s/UsePrivilegeSeparation.*/UsePrivilegeSeparation no/g" /etc/ssh/sshd_config \
    && sed -i 's/PermitRootLogin without-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
    && sed -ri 's/^session\s+required\s+pam_loginuid.so$/session optional pam_loginuid.so/' /etc/pam.d/cron \
    && sed -ri 's/^session\s+required\s+pam_loginuid.so$/session optional pam_loginuid.so/' /etc/pam.d/sshd \
    && ln -s /usr/share/lmod/lmod/init/env_modules_python.py /usr/share/lmod/lmod/init/python \
    && touch /root/.Xauthority \
    && true

# Add Users and Groups
RUN groupadd sdss
RUN useradd -g sdss stui_user \
    && chsh -s /bin/bash stui_user \
    && passwd -d stui_user \
    && mkdir /home/stui_user \
    && mkdir /home/stui_user/.subversion \
    && addgroup stui_user sdss \
    && addgroup stui_user staff \
    && true

ADD users/stui_user/etc/motd /etc/motd
ADD users/stui_user/home/stui_user /home/stui_user/
RUN chmod -x /etc/update-motd.d/* \
    && chmod +x /home/stui_user/crontab/svn/* \
    && chmod +x /home/stui_user/crontab/git/* \
    && echo "stui_user       ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers


ENV SSH_KEY_JOEL ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDHQ/qcYdnnlKUy295NZQBrq3kiv4u34W+8AEPRe35/RppAy/wYmaTMK0oE7NXFnatxA+7sFz8BOfHI4si5MHt/wn8tgB8XteSMmYFgLi9BExMlx+7q9jt6tMzUy7gYdx6sh9KCS5hoH8HSt2E5MoZK57UqUMMMaBfcWvBYyt0y+WXujTN1AliAgnI3VdywZP8/k4UQ4K+FwTYSOt3bSzmtD/YdD8ngk+2DSpjASl/1Z16ESz6jYJxqvBhdgT81Q6+Bp8/K8NQrXfKJHNWW1P3yTe5m+DI7LvDu8Bae3fSMvuq4/Vce0Et1HTEvVebCinPO0xmrg3j9LvFtqvVjZjvl joel@dhn

ENV SSH_KEY ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDU1+39M+PZTuT8jGHW4XJuLxMY5qd/N57xGTfNjE0evpWR0LWs+8NbEPq/hC4nlAzy/Bi5+2+f4jpfh3U8OMtajtXPG6Q3e85Ut6IPJI2I4ttqzuPA3jmADMzPmLehxUuG/ro8tlzuW03GAxS+76W49qjuS7HGAU4KQZUQK0apaktz4Ss2z/I7E3jZquLh5cq33uSBkFcDfImMuSOhtt/MoOO3sID7LcuV/ZKDynUsL+lorwoNvoygtmEk4bBooyR65RSPBaiPbNjFjHEfFinZdVyVSawySEGxjImAAV5W9/r1PPVjW3dNWIckAoeWYGBATYoPgJ36+35kmsSPWlTz albireo@D-69-91-153-24.dhcp4.washington.edu

# ========================================================
# HOST > PYTHON
# ========================================================

RUN apt-get update \
    && apt-get install -y python-software-properties \
    && apt-get install -y python2.7 \
	&& rm -rf /var/lib/apt/lists/* \
    && locale-gen en_US.UTF-8

ADD host/stui/etc/timezone /etc/timezone

RUN locale-gen en_US.UTF-8 \
    && dpkg-reconfigure -f noninteractive tzdata

EXPOSE 22

CMD ["/tmp/bin/start_services"]

