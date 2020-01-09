FROM node:4.3.2

# Apt-get install should not cache
COPY 02nocache /etc/apt/apt.conf.d/02nocache

# Hopefully, there will be no
COPY 01_nodoc /etc/dpkg/dpkg.cfg.d/01_nodoc

ENV gid=1000 uid=1000

RUN apt-get update && apt-get install -y sudo python-pip python-dev jq zip && \
    pip install awscli && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get remove python-dev -y && \
    apt-get autoremove -y && \
    # adds the group
    groupadd -g $gid dev && \
    # creates the user named dev with the right uid and gid
    useradd -g $gid -u $uid -m dev && \
    # allow the dev user use sudo without a password
    echo "dev ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    npm install --no-spin --loglevel warn -g mocha@3.0.2 sequelize-cli@2.4.0 \
    istanbul@0.4.5

COPY entrypoint.sh /home/dev/entrypoint.sh
RUN chown dev:dev /home/dev/entrypoint.sh

# default user to run commands on the container, also all RUN commands from this point are executed
# with this user
USER dev

WORKDIR /home/dev

RUN chmod +x /home/dev/entrypoint.sh

CMD ["./entrypoint.sh"]
