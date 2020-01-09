FROM ubuntu
MAINTAINER Richard Weber <riche.weber@gmail.com>

RUN apt-get update && apt-get install -y texlive-latex-extra latexmk texlive-lang-finnish texlive-lang-swedish

# Mount your project to /src
WORKDIR /src

ENTRYPOINT ["/bin/sh","-c", "pdflatex"]

CMD ["hello.tex"]
