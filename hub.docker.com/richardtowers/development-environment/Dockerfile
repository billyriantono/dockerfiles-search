FROM silex/emacs:26.1-alpine-dev as emacs

# ---------------------

FROM alpine:3.7

COPY --from=0 /usr/local /usr/local

RUN apk add --no-cache \
        alsa-lib \
        aspell \
        aspell-en \
        curl \
        desktop-file-utils \
        gconf \
        giflib \
        gnupg \
        gtk+3.0 \
        libcanberra-gtk3 \
        librsvg \
        libxpm \
        openssh-client \
        python \
        ruby \
        tiff \
    && /bin/true

ENV EMACS_BRANCH="emacs-26.1"
ENV EMACS_VERSION="26.1"
ENV PATH="/root/.cask/bin:$PATH"

COPY --from=0 /root/.cask /root/.cask
COPY .emacs.d /root/.emacs.d

WORKDIR /root/.emacs.d
RUN cask install

WORKDIR /root/work

ENTRYPOINT ["emacs"]
CMD ["."]

