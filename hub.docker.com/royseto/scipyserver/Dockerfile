FROM royseto/scipystack_pg

MAINTAINER roy.seto@gmail.com

VOLUME /notebooks
WORKDIR /notebooks

EXPOSE 8888

# You can mount your own SSL certs as necessary here
# $PASSWORD will get `unset` within notebook.sh, turned into an IPython style hash
ENV PEM_FILE=/home/dev/key.pem \
    PASSWORD="Dont make this your default" \
    USE_HTTP=0 \
    LD_LIBRARY_PATH=/usr/local/pgsql/lib \
    PATH=/usr/local/pgsql/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN useradd dev -u 1000 -c "developer account" -d /home/dev -s /bin/bash -g users -G sudo --no-create-home
RUN mkdir -p /home/dev && /bin/chown dev:users /home/dev

# Enable passwordless sudo for users in the sudo group.
RUN sed -ie '/sudo/ s/ALL$/NOPASSWD: ALL/' /etc/sudoers

ADD notebook.sh /
RUN chown dev:users /notebook.sh && chmod u+x /notebook.sh

USER dev

CMD ["/notebook.sh"]
