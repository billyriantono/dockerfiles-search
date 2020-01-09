FROM antergos/archlinux-systemd

# RUN pacman -Syyu --noconfirm
# RUN pacman -S nginx dos2unix openssh sudo iputils vim iproute2 --noconfirm

# RUN ln -sf /dev/stdout /var/log/nginx/access.log \
#     && ln -sf /dev/stderr /var/log/nginx/error.log


# COPY ./tools/start-packages /usr/local/bin/start-packages
# RUN dos2unix /usr/local/bin/start-packages \
#     && chmod +x /usr/local/bin/start-packages 
# 
# COPY ./tools/create-gpg /usr/local/bin/create-gpg
# RUN dos2unix /usr/local/bin/create-gpg \
#     && chmod +x /usr/local/bin/create-gpg
# 
# COPY ./tools/sync-repo /usr/local/bin/sync-repo
# RUN dos2unix /usr/local/bin/sync-repo \
#     && chmod +x /usr/local/bin/sync-repo

# COPY ./nginx/pacman /etc/nginx/sites-available/default
# RUN dos2unix /etc/nginx/sites-available/default

ENV REPO_PASSWD=Mudar123

RUN useradd -ms /bin/bash repo && echo "repo:${REPO_PASSWD}" | chpasswd
RUN echo "repo ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN mkdir -p /etc/i9corp/packages/dist/x86_64 \
    && mkdir -p /etc/i9corp/packages/dist/i686

RUN chown -R repo:repo /etc/i9corp

VOLUME [ "/etc/i9corp" ]

EXPOSE 22
EXPOSE 80
EXPOSE 443

RUN touch /var/log/test.log

CMD ["/usr/sbin/init"]
