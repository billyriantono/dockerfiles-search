FROM paperist/alpine-texlive-ja

# COPY .latexmkrc /workdir
RUN apk --no-cache add \
    libxaw-dev \
    openssh \
    git \
    wget

RUN tlmgr update --self --all \
    && tlmgr install siunitx

COPY ./.latexmkrc /root/
