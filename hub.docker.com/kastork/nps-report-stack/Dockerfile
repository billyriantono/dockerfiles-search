FROM haskell:8
# (debian jessie)

MAINTAINER Kirk Stork <kastork@nps.edu>

ENV PANDOC_VERSION "1.18"

# install pandoc

RUN cabal update && cabal install pandoc-${PANDOC_VERSION}


# install latex packages

RUN apt-get update -y
RUN apt-get install -y --no-install-recommends texlive-full \
    fontconfig

WORKDIR /source

COPY NPS_LaTeX_Template/nps_sf298.sty /root/texmf/tex/latex/nps/nps_sf298.sty
COPY NPS_LaTeX_Template/nps_thesis.bst /root/texmf/bibtex/bst/nps/nps_thesis.bst
COPY NPS_LaTeX_Template/npsreport.cls /root/texmf/tex/latex/nps/npsreport.cls
COPY NPS_LaTeX_Template/acronyms.tex /root/texmf/tex/latex/nps/acronyms.tex

CMD ["/bin/bash"]