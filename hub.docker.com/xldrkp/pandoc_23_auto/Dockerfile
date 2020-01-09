# Datei Dockerfile
FROM haskell
# Pakete installiren
RUN apt-get update -y && \
    apt-get install -y -o Acquire::Retries=10 \
                    --no-install-recommends \
        texlive-latex-recommended \
        texlive-latex-extra \
        texlive-fonts-recommended \
        texlive-lang-german \
        texlive-pstricks \
        texlive-font-utils \
        texlive-xetex \
        texlive-luatex \
        lmodern \
        imagemagick \
        unzip \
        python3 \
        ghostscript \
        subversion \
        joe \
        vim \
        less && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*

# Pandoc installiren
RUN cabal new-update && \
    cabal new-install pandoc-2.5 pandoc-citeproc && \
    ln -s /root/.cabal/bin/pandoc /usr/bin/pandoc

# Mitteleuropäische Zeitzone
# (siehe https ://serverfault.com/questions/683605)
RUN cp /usr/share/zoneinfo/Europe/Berlin /etc/localtime

# Fonts für LaTeX installieren
# ADD myfonts.tgz /usr/local/share/texmf
# RUN texhash

# Volume /data, bei docker run mit dem Arbeitsverzeichnis
# verbinden , also: docker run -v $( pwd ) :/data
WORKDIR /data
VOLUME ["/data"]
CMD ["/bin/bash"]
