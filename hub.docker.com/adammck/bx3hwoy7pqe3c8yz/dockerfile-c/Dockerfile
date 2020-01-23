FROM clearlinux:base
RUN swupd bundle-add --no-boot-update desktop texlive

WORKDIR /src

CMD ["latexmk", "-pdf", "-outdir=./build"]
