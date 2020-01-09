FROM debian:buster-slim

# RUN ln -snf /usr/share/zoneinfo/Etc/UTC /etc/localtime \
#     && echo "Etc/UTC" > /etc/timezone

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
    biber \
    curl \
    make \
    texlive-bibtex-extra \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-latex-extra \
    texlive-latex-recommended \
    texlive-publishers \
    texlive-science tex-gyre \
    xzdec \
    && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/bin/bash", "-c", "/usr/bin/make -C /target; /usr/bin/make -C /target clean"]
