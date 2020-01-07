FROM ubuntu:18.04

RUN apt-get update

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
          dialog \
          git \
          gitg \
          asciidoctor \
          calibre \
          ruby \
          firefox \
          openssh-client \
          wget \
          gconf2 \
          gconf-service \
          libnotify4 \
          gvfs-bin \
          libxkbfile1 \
          libcurl4 \
          libxss1

RUN wget -O "atom-latest.deb" https://atom.io/download/deb && \
    dpkg -i atom-latest.deb && \
    rm atom-latest.deb

RUN gem install asciidoctor-bibtex
RUN gem install asciidoctor-pdf --pre
RUN gem install rouge
RUN gem install pygments.rb
RUN gem install coderay
RUN gem install unicode_utils

RUN apm install asciidoc-assistant
RUN apm install autocomplete-asciidoc
RUN apm install asciidoc-preview
RUN apm install language-asciidoc
RUN apm install asciidoc-image-helper
RUN useradd -d /home/atom -m atom

USER atom

CMD ["/usr/bin/atom","-f"]
