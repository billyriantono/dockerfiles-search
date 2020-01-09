FROM circleci/golang
RUN sudo apt-get install -y upx && sudo apt-get clean
RUN go get github.com/chzyer/readline &&\
    go get github.com/valyala/fasttemplate &&\
    go get github.com/kr/pty &&\
    go get github.com/pwaller/goupx &&\
    go get github.com/godbus/dbus &&\
    go get github.com/coreos/go-systemd/daemon &&\
    go get github.com/coreos/go-systemd/util &&\
    go get github.com/coreos/go-systemd/journal &&\
    go get github.com/urfave/cli

