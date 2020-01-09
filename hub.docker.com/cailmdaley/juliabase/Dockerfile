FROM julia:1.3
ENV JULIAVERSION 1.3

# apt-get dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
        ca-certificates \
        cmake \
        curl \
        gcc \
        git \
        ffmpeg \
        gfortran \
        qt5-default \
        make \
        man \
        ruby \
        tar \
        vim \
        wget \
    && rm -rf /var/lib/apt/lists/*

# setup an unprivileged user
ENV IMAGEUSER imageuser
ENV HOME /home/$IMAGEUSER
RUN adduser --disabled-password --gecos "Default user" $IMAGEUSER \
    && chown -R $IMAGEUSER $HOME

# create non-home user-writable $SRC directory for software
ENV SRC /src
RUN mkdir -p $SRC/bin
ENV PATH="$SRC/bin:$PATH"

# setup Tex distribution:
COPY --chown=1000 .panrun $SRC/.panrun
COPY --chown=1000 tinytex_packagelist.txt $SRC/.tinytex/
    # TinyTex
RUN wget -qO- "https://yihui.name/gh/tinytex/tools/install-unx.sh" | sh \
        && $HOME/.TinyTeX/bin/x86_64-linux/tlmgr install $(cat $SRC/.tinytex/tinytex_packagelist.txt) \
        && mv $HOME/.TinyTeX/* $SRC/.tinytex \
        && ln -s $SRC/.tinytex/bin/x86_64-linux/* $SRC/bin \
    # pandoc:
    && wget https://github.com/jgm/pandoc/releases/download/2.7.3/pandoc-2.7.3-1-amd64.deb \
        && dpkg -i pandoc-2.7.3-1-amd64.deb \
        && rm pandoc-2.7.3-1-amd64.deb \
    # link panrun:
    && ln -s $SRC/.panrun/panrun $SRC/bin/ \
    # finally, clean up $HOME and make sure user owns src
    && rm -rf $HOME/* \
    && chown -R $IMAGEUSER $SRC


# switch to user
USER $IMAGEUSER
WORKDIR $HOME

# initialize Julia user environment in $SRC
ENV JULIA_DEPOT_PATH $SRC/.julia
COPY --chown=1000 Project.toml $JULIA_DEPOT_PATH/environments/v$JULIAVERSION/
RUN julia -e 'using Pkg; pkg"instantiate; precompile"'
