FROM debian:latest

LABEL "com.github.actions.name"="Run latex"
LABEL "com.github.actions.description"="Compile latex files"
LABEL "com.github.actions.icon"="paperclip"
LABEL "com.github.actions.color"="blue"

RUN set -eux; \
    apt-get update; \
    apt-get install --no-install-recommends -y \
        texlive \
        texlive-generic-recommended \
        texlive-latex-extra \
        texlive-math-extra \
        texlive-lang-english \
        texlive-lang-german \
        texlive-science \
        texlive-publishers \
        latexmk \
    ; \
    rm -rf /var/lib/apt/lists/*
