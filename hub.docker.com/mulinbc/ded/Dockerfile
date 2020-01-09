FROM mulinbc/sshd

RUN dnf update -y && \
    dnf install -y g++ gdb go make && \
    # install go tools
    go get -x -d github.com/stamblerre/gocode 2>&1 && \
    go build -o gocode-gomod github.com/stamblerre/gocode && \
    mv gocode-gomod $GOPATH/bin/ && \
    go get -u -v \
    github.com/acroca/go-symbols \
    github.com/alecthomas/gometalinter \
    github.com/cweill/gotests/... \
    github.com/davidrjenni/reftools/cmd/fillstruct \
    github.com/derekparker/delve/cmd/dlv \
    github.com/fatih/gomodifytags \
    github.com/godoctor/godoctor \
    github.com/golangci/golangci-lint/cmd/golangci-lint \
    github.com/haya14busa/goplay/cmd/goplay \
    github.com/josharian/impl \
    github.com/mdempsky/gocode \
    github.com/mgechev/revive \
    github.com/ramya-rao-a/go-outline \
    github.com/rogpeppe/godef \
    github.com/sqs/goreturns \
    github.com/uudashr/gopkgs/cmd/gopkgs \
    github.com/zmb3/gogetdoc \
    golang.org/x/lint/golint \
    golang.org/x/tools/cmd/goimports \
    golang.org/x/tools/cmd/gopls \
    golang.org/x/tools/cmd/gorename \
    golang.org/x/tools/cmd/guru \
    honnef.co/go/tools/... 2>&1 && \
    # clean
    dnf clean all && rm -rf /var/cache/dnf/*
