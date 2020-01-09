FROM ubuntu:18.04
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -yq update && apt-get install -qy --no-install-recommends lsb-release 

RUN echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | debconf-set-selections && \
    echo "deb http://archive.ubuntu.com/ubuntu/ $(lsb_release -sc) multiverse" | tee -a /etc/apt/sources.list && \
    echo "deb-src http://archive.ubuntu.com/ubuntu/ $(lsb_release -sc) multiverse" | tee -a /etc/apt/sources.list && \
    apt-get -yq update && \
    apt-get -y dist-upgrade && \
    apt-get install -qy --no-install-recommends \
      make unzip curl perl ttf-mscorefonts-installer \
      latexmk biber python-pygments gnuplot cm-super \
      graphviz dot2tex ttf-dejavu \
      texlive-xetex texlive-generic-extra texlive-fonts-recommended lmodern fonts-liberation texlive-bibtex-extra \
      texlive-lang-cyrillic texlive-latex-extra texlive-science texlive-pstricks texlive-publishers && \
    apt-get purge -qy texlive-latex-base-doc texlive-latex-extra-doc texlive-pictures-doc texlive-pstricks-doc texlive-science-doc && \
    apt-get autoclean -qy && \
    apt-get autoremove -qy && \
    apt-get install -qy gcc default-jre umlet && \
    fc-cache -vf

RUN cpan -Ti YAML::Tiny && \
    cpan -Ti File::HomeDir && \
    cpan -Ti Unicode::GCString && \
    cpan -Ti Log::Log4perl && \
    cpan -Ti Log::Dispatch
  
ADD PSCyr.zip install.sh /tmp/
ADD latex2pdf /usr/bin/
ADD umlet_convert /usr/bin/
RUN bash /tmp/install.sh

ADD latexindent.pl defaultSettings.yaml install_indent.sh /indent/
ADD LatexIndent /indent/LatexIndent

RUN bash /indent/install_indent.sh

WORKDIR /data
VOLUME ["data"]
