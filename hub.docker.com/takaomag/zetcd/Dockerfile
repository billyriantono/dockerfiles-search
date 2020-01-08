# zetcd

FROM takaomag/base:2017.12.18.09.45

ENV \
    X_DOCKER_REPO_NAME=zetcd \
#    X_ZETCD_VERSION=0.0.4
    X_ZETCD_GIT_CHECKOUT=master


RUN \
    echo "2016-03-08-0" > /dev/null && \
    export TERM=dumb && \
    export LANG='en_US.UTF-8' && \
    source /opt/local/bin/x-set-shell-fonts-env.sh && \
: && \
    echo -e "${FONT_INFO}[INFO] Update package database${FONT_DEFAULT}" && \
    reflector --latest 100 --verbose --sort score --save /etc/pacman.d/mirrorlist && \
    sudo -u nobody yaourt -Syy && \
    echo -e "${FONT_SUCCESS}[SUCCESS] Update package database${FONT_DEFAULT}" && \
: && \
#    echo -e "${FONT_INFO}[INFO] Refresh package developer keys${FONT_DEFAULT}" && \
#    pacman-key --refresh-keys && \
#    echo -e "${FONT_SUCCESS}[SUCCESS] Refresh package developer keys${FONT_DEFAULT}" && \
: && \
    REQUIRED_PACKAGES=("git" "go") && \
: && \
    echo -e "${FONT_INFO}[INFO] Install required packages [${REQUIRED_PACKAGES[@]}]${FONT_DEFAULT}" && \
    sudo -u nobody yaourt -S --needed --noconfirm --noprogressbar "${REQUIRED_PACKAGES[@]}" && \
    echo -e "${FONT_SUCCESS}[SUCCESS] Install required packages [${REQUIRED_PACKAGES[@]}]${FONT_SUCCESS}" && \
: && \
    echo -e "${FONT_INFO}[INFO] Install zetcd-${X_ZETCD_VERSION}${X_ZETCD_GIT_CHECKOUT}${FONT_DEFAULT}" && \
    export GOPATH=/opt/local && \
    if [[ "${X_ZETCD_VERSION}" ]];then\
      mkdir -p /opt/local/src/github.com/coreos && \
      curl --silent --location --fail --retry 5 "https://github.com/coreos/zetcd/archive/v${X_ZETCD_VERSION}.tar.gz" | tar xz -C /opt/local/src/github.com/coreos && \
      mv /opt/local/src/github.com/coreos/zetcd-${X_ZETCD_VERSION} /opt/local/src/github.com/coreos/zetcd;\
    else\
      git clone -b ${X_ZETCD_GIT_CHECKOUT} https://github.com/coreos/zetcd.git /opt/local/src/github.com/coreos/zetcd; \
#      cd /opt/local/src/github.com/coreos/zetcd; \
#      git checkout "${X_ZETCD_GIT_CHECKOUT}";\
    fi && \
    go get -d github.com/coreos/zetcd/... && \
    go install github.com/coreos/zetcd/cmd/zetcd && \
    cd /tmp && \
    rm -rf /opt/local/src/* && \
    yaourt -Rsn --noconfirm go && \
    echo -e "${FONT_SUCCESS}[SUCCESS] Install zetcd-${X_ZETCD_VERSION}${X_ZETCD_GIT_CHECKOUT}${FONT_DEFAULT}" && \
: && \
    /opt/local/bin/x-archlinux-remove-unnecessary-files.sh && \
#    pacman-optimize && \
    rm -f /etc/machine-id

EXPOSE \
    2181

ENTRYPOINT ["/opt/local/bin/zetcd"]

CMD ["--zkaddr", "0.0.0.0:2181", "--endpoints", "localhost:2379", "-logtostderr", "-stderrthreshold", "INFO"]
