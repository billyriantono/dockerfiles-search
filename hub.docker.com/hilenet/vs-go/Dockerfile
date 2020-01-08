FROM golang:latest

# https://github.com/Microsoft/vscode-go/wiki/Go-tools-that-the-Go-extension-depends-on
RUN go get github.com/ramya-rao-a/go-outline \
            github.com/acroca/go-symbols \
            github.com/mdempsky/gocode \
            github.com/rogpeppe/godef \
            golang.org/x/tools/cmd/godoc \
            github.com/zmb3/gogetdoc \
            golang.org/x/lint/golint \
            github.com/fatih/gomodifytags \
            golang.org/x/tools/cmd/gorename \
            sourcegraph.com/sqs/goreturns \
            golang.org/x/tools/cmd/goimports \
            github.com/cweill/gotests/... \
            golang.org/x/tools/cmd/guru \
            github.com/josharian/impl \
            github.com/haya14busa/goplay/cmd/goplay \
            github.com/uudashr/gopkgs/cmd/gopkgs \
            github.com/davidrjenni/reftools/cmd/fillstruct \
            github.com/alecthomas/gometalinter \
  && gometalinter --install \
# for debugging
  && go get github.com/go-delve/delve/cmd/dlv \
  && go get github.com/golang/dep/cmd/dep

