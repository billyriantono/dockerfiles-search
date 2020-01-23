# --- base image: ubuntu 18.04 ---
FROM ubuntu:18.04

# --- install base packages ---
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y \
    wget \
    curl \
    xz-utils \
    git \
    build-essential

RUN apt-get clean

# --- install go ---
ENV GO_VERSION 1.9.1
ENV PATH $PATH:/usr/local/go/bin
ENV PATH $PATH:~/go/bin
RUN curl -O https://storage.googleapis.com/golang/go${GO_VERSION}.linux-amd64.tar.gz \
	&& tar -xvf go${GO_VERSION}.linux-amd64.tar.gz \
	&& mv go /usr/local

# --- install github release ---
RUN go get -u github.com/tcnksm/ghr

# --- install texlive and pandoc ---
RUN apt-get install -y texlive
RUN apt-get install -y pandoc

# -- basic configuration latexmkrc (customization) ---
RUN touch /root/.latexmkrc
RUN echo "@generated_exts = ('aux', 'bcf', 'fls', 'idx', 'ind', 'lof', 'lot', 'out', 'toc', 'nav', 'snm', 'dvi');" >>  /root/.latexmkrc
RUN echo "\$pdflatex = 'pdflatex -halt-on-error --shell-escape -synctex=1';" >> /root/.latexmkrc
RUN echo "\$pdf_mode = 1;" >> /root/.latexmkrc
RUN echo "\$bibtex_use = 1;" >> /root/.latexmkrc
RUN echo "\$clean_ext = 'synctex.gz';" >> /root/.latexmkrc