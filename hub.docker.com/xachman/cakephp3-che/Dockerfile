FROM xachman/cakephp3

EXPOSE 4403 80 9876 22

LABEL che:server:80:ref=apache2 che:server:80:protocol=http che:server:9876:ref=codeserver che:server:9876:protocol=http

RUN apt-get update && \
    apt-get -y install sudo openssh-server git procps wget unzip mc curl locales subversion software-properties-common python-software-properties && \
    mkdir /var/run/sshd && \
    sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd && \
    echo "%sudo ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd -u 1000 -G users,sudo -d /home/user --shell /bin/bash -m user && \
    echo "secret\nsecret" | passwd user && \
    apt-get clean && \
    apt-get -y autoremove && \
    rm -rf /var/lib/apt/lists/*

USER user

ENV LANG en_GB.UTF-8
ENV LANG en_US.UTF-8
RUN sudo locale-gen en_US.UTF-8 && \
    svn --version && \
    sed -i 's/# store-passwords = no/store-passwords = yes/g' /home/user/.subversion/servers && \
    sed -i 's/# store-plaintext-passwords = no/store-plaintext-passwords = yes/g' /home/user/.subversion/servers

WORKDIR /projects

COPY apache2.conf /etc/apache2

CMD sudo /usr/sbin/sshd -D && \
    tail -f /dev/null