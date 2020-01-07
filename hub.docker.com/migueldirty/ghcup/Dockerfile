FROM debian:buster

ARG GHC_VERSION=
ARG USER=haskeller
ENV PATH="/home/${USER}/.cabal/bin:/home/${USER}/.ghcup/bin:${PATH}"

RUN echo "Dear Sir or Madam,"                           && \
    echo ""                                             && \
    echo "Welcome to Miguel's Docker Builder."          && \
    echo "We are building a fresh Haskell Environment." && \
    echo ""                                             && \
    echo "This Build is parametrized as follows:"       && \
    echo ""                                             && \
    echo "GHC_VERSION = ${GHC_VERSION}"                 && \
    echo "PATH        = ${PATH}"                        && \
    echo "USER        = ${USER}"                        && \
    echo ""                                             && \
    echo "[STEP 1 : INSTALLING DEPS VIA APT]"           && \
    echo ""                                             && \
    apt-get update                                      && \
    apt-get install -y  \
        curl            \
        xz-utils        \
        gcc             \
        make            \
        libtinfo5       \
        libgmp-dev      \
        zlib1g-dev                                      && \
    echo ""                                             && \
    echo "[STEP 2 : CREATE USER & HOMEDIR]"             && \
    echo ""                                             && \
    useradd -ms /bin/bash ${USER}                       && \
    echo ""                                             && \
    echo "[STEP 3 : DOWNLOAD AND INSTALL ghcup]"        && \
    echo ""                                             && \
    su ${USER} -c "mkdir -p ~/.ghcup/bin"               && \
    su ${USER} -c "curl https://gitlab.haskell.org/haskell/ghcup/raw/master/ghcup > ~/.ghcup/bin/ghcup" && \
    su ${USER} -c "chmod +x ~/.ghcup/bin/ghcup"         && \
    echo ""                                             && \
    echo "[STEP 4 : INSTALL ghc VIA ghcup]"             && \
    echo ""                                             && \
    su ${USER} -c "ghcup install ${GHC_VERSION}"        && \
    su ${USER} -c "ghcup set ${GHC_VERSION}"            && \
    echo ""                                             && \
    echo "[STEP 5 : INSTALL & UPDATE cabal]"            && \
    echo ""                                             && \
    su ${USER} -c "ghcup install-cabal"                 && \
    su ${USER} -c "cabal update"                        && \
    su ${USER} -c "cabal new-install cabal-install"     && \
    echo ""                                             && \
    echo "[FINISHED! THANK YOU FOR YOUR PATIENCE]"      && \
    echo ""                                             

USER ${USER}
ENV PATH="/home/${USER}/.cabal/bin:/home/${USER}/.ghcup/bin:${PATH}"
RUN cabal install ghcid
RUN cabal install hlint
