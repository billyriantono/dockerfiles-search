FROM tianon/latex

RUN apt-get update && apt-get install -y \
	wget \
	python \
	python-pip \
	python-pygments \
	&& rm -rf /var/lib/apt/lists/*

RUN cd ~ \
	&& wget http://mirrors.ctan.org/fonts/ulsy.zip \
	&& unzip ulsy.zip && rm ulsy.zip\
	&& cd ulsy \
	&& latex ulsy.ins \
	&& mkdir -p /usr/share/texlive/texmf-dist/tex/latex/ulsy \
	&& mkdir -p /usr/share/texlive/texmf-dist/fonts/tfm/public/ulsy \
	&& mkdir -p /usr/share/texlive/texmf-dist/fonts/source/public/ulsy \
	&& mv ulsy.sty /usr/share/texlive/texmf-dist/tex/latex/ulsy/ \
	&& mv Uulsy.fd /usr/share/texlive/texmf-dist/tex/latex/ulsy/ \
	&& mv ulsy10.tfm /usr/share/texlive/texmf-dist/fonts/tfm/public/ulsy/ \
	&& mv ulsy10.mf /usr/share/texlive/texmf-dist/fonts/source/public/ulsy/ \
	&& texhash \
	&& cd ~ \
	&& rm -r ulsy
