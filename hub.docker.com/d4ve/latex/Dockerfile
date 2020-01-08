FROM ubuntu:rolling as latex

RUN apt-get update

RUN apt-get --yes --no-install-recommends install texlive texlive-latex-base texlive-latex-extra texlive-base texlive-bibtex-extra  texlive-extra-utils

RUN apt-get --yes --no-install-recommends install texlive-fonts-recommended texlive-font-utils texlive-fonts-extra texlive-formats-extra  

RUN apt-get --yes --no-install-recommends install texlive-lang-english texlive-lang-german texlive-lang-french texlive-lang-cyrillic  texlive-lang-chinese texlive-lang-japanese texlive-lang-italian

RUN apt-get --yes --no-install-recommends install texlive-science texlive-publishers texlive-pictures texlive-htmlxml  

RUN apt-get --yes --no-install-recommends install build-essential

RUN apt-get --yes --no-install-recommends install biber

RUN apt-get --yes --no-install-recommends install wget

RUN wget https://ctan.org/tex-archive/macros/latex/contrib/javadoc/tex/javadoc.sty; mv javadoc.sty /usr/share/texlive/texmf-dist/tex/latex

RUN mktexlsr

RUN apt-get clean  \
    && rm -rf /var/lib/apt/lists/*

FROM openjdk:jre-alpine

RUN apk update \
	&& apk add ttf-dejavu \
	&& wget -q http://umlet.com/umlet_13_3/umlet_13.3.zip \
	&& unzip -q umlet_13.3.zip 
COPY --from=latex / /
