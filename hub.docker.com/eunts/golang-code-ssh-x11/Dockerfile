# use
#     docker run --rm -ti -v $(pwd):/app/ eunts/golang-code-ssh-x11:latest
# to run

FROM golang:1.11.4-stretch


# ssh & run
COPY run.sh /bin/run
RUN apt-get update && \
    apt-get install -y openssh-server && \
    passwd -d root && \
    chmod 0700 /bin/run && \
    sed -ri 's/^\s*(PermitRootLogin)/#\1/'                   /etc/ssh/sshd_config && \
    echo "PermitRootLogin yes"                           >> /etc/ssh/sshd_config && \
#
    sed -ri 's/^\s*(X11Forwarding)/#\1/'                     /etc/ssh/sshd_config && \
    echo "X11Forwarding yes"                             >> /etc/ssh/sshd_config && \
#
    sed -ri 's/^\s*(X11DisplayOffset)/#\1/'                 /etc/ssh/sshd_config && \
    echo "X11DisplayOffset 10"                           >> /etc/ssh/sshd_config && \
#
    sed -ri 's/^\s*(X11UseLocalhost)/#\1/'                  /etc/ssh/sshd_config && \
    echo "X11UseLocalhost no"                            >> /etc/ssh/sshd_config && \
#
    sed -ri 's/^\s*(ChallengeResponseAuthentication)/#\1/'  /etc/ssh/sshd_config && \
    echo "ChallengeResponseAuthentication no"            >> /etc/ssh/sshd_config && \
#
    sed -ri 's/^\s*(PasswordAuthentication)/#\1/'           /etc/ssh/sshd_config && \
    echo "PasswordAuthentication yes"                    >> /etc/ssh/sshd_config && \
#
    sed -ri 's/^\s*(UsePAM)/#\1/'                           /etc/ssh/sshd_config && \
    echo "UsePAM no"                                     >> /etc/ssh/sshd_config && \
#
    sed -ri 's/^\s*(PermitEmptyPasswords)/#\1/'             /etc/ssh/sshd_config && \
    echo "PermitEmptyPasswords yes"                      >> /etc/ssh/sshd_config && \
#
    sed -ri 's/^\s*(Compression)/#\1/'                      /etc/ssh/sshd_config && \
    echo "Compression no"                                >> /etc/ssh/sshd_config && \
    mkdir /var/run/sshd

# code 
RUN echo "deb [arch=amd64] http://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list && \
    curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > /tmp/microsoft.gpg && \
    install -o root -g root -m 644 /tmp/microsoft.gpg /etc/apt/trusted.gpg.d/ && \
    apt-get update && \
    apt-get install -y code libasound2 sudo bash && \
    useradd --create-home -g root --shell /bin/bash code && \
    passwd -d code && \
# clear motd
    echo > /etc/motd && \
# set some stuff up for go
    echo "export GOROOT=/usr/local/go" >> /etc/bash.bashrc && \
    echo "export GOPATH=/go" >> /etc/bash.bashrc && \
    echo "export PATH=\$GOROOT/bin:\$GOPATH/bin:\$PATH" >> /etc/bash.bashrc && \
# install extensions
    sudo -u code code --install-extension ms-vscode.Go && \
    sudo -u code code --install-extension 766b.go-outliner && \
# install dependencies
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/mdempsky/gocode && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/uudashr/gopkgs/cmd/gopkgs && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/ramya-rao-a/go-outline && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/acroca/go-symbols && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get golang.org/x/tools/cmd/guru && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get golang.org/x/tools/cmd/gorename && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/go-delve/delve/cmd/dlv && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/stamblerre/gocode && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/rogpeppe/godef && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/sqs/goreturns && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get golang.org/x/lint/golint && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/cweill/gotests/... && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/fatih/gomodifytags && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/josharian/impl && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/davidrjenni/reftools/cmd/fillstruct && \
    sudo -u code GOPATH=/go /usr/local/go/bin/go get github.com/haya14busa/goplay/cmd/goplay && \
# fix permissions
    chmod -R 0770 /home/code

EXPOSE 22

ENV RUN_USER=code
CMD [ "run", "/usr/sbin/sshd", "-D", "-f", "/etc/ssh/sshd_config" ]