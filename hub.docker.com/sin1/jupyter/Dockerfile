FROM	debian:9
ENV	DEBIAN_FRONTEND noninteractive
# atp-get
RUN	apt-get update && \
	apt-get install -y apt-utils libtool pkg-config autoconf rake git wget curl && \
	apt-get install -y libczmq4 libczmq-dev libczmq-dbg && \
	apt-get install -y libzmq5 libzmq5-dev libzmq5-dbg && \
	apt-get install -y python-pip libpq-dev python-dev python3-pip python3-dev libunwind-dev && \
	apt-get install -y r-base r-base-dev libssh2-1-dev libcurl4-openssl-dev libssl-dev && \
	apt-get install -y ruby ruby-dev && \
	apt-get install -y octave && \
	apt-get install -y swi-prolog && \
	apt-get install -y libtinfo-dev libcairo2-dev libpango1.0-dev libmagic-dev libblas-dev liblapack-dev libffi-dev && \
	apt-get upgrade -y && \
	apt-get clean && rm -rf /var/lib/apt/lists/* && \
## ZeroMQ
#	cd /root && \
#	git clone --depth=1 https://github.com/zeromq/libzmq && \
#	git clone --depth=1 https://github.com/zeromq/czmq && \
#	cd /root/libzmq && ./autogen.sh && ./configure --prefix=/usr && make -j8 && make install && \
#	cd /root/czmq   && ./autogen.sh && ./configure --prefix=/usr && make -j8 && make install && \
#	cd /root && \
#	rm -rf /root/libzmq && \
#	rm -rf /root/czmq && \
# Jupyter & Python
	pip3 install --upgrade pip && \
	pip3 install jupyterlab widgetsnbextension && \
	jupyter serverextension enable --py jupyterlab --sys-prefix && \
	pip2 install --upgrade pip && \
	python2 -m pip install ipykernel && \
	python2 -m ipykernel install && \
	mkdir /notebook && \
	jupyter notebook --allow-root --generate-config && \
	echo "c.NotebookApp.allow_root = True" >> /root/.jupyter/jupyter_notebook_config.py && \
	echo "c.NotebookApp.ip = '*'" >> /root/.jupyter/jupyter_notebook_config.py && \
	echo "c.NotebookApp.open_browser = False" >> /root/.jupyter/jupyter_notebook_config.py && \
	echo "c.NotebookApp.notebook_dir = '/notebook'" >> /root/.jupyter/jupyter_notebook_config.py && \
	echo "c.NotebookApp.token = 'pass'" >> /root/.jupyter/jupyter_notebook_config.py && \
	pip3 install jupyter_contrib_nbextensions && \
	jupyter nbextensions_configurator enable && \
# R
	echo "options(repos='http://cran.ism.ac.jp/')" > install.R && \
	echo "install.packages(c('repr', 'IRdisplay', 'evaluate', 'crayon', 'devtools', 'pbdZMQ', 'uuid', 'digest'))" >> install.R && \
	echo "devtools::install_github('IRkernel/IRkernel')" >> install.R && \
	echo "IRkernel::installspec()" >> install.R && \
	R --vanilla -q < install.R  && \
	rm -rf install.R && \
# Julia
	wget https://julialang-s3.julialang.org/bin/linux/x64/0.6/julia-0.6.0-linux-x86_64.tar.gz && \
	tar xf julia-0.6.0-linux-x86_64.tar.gz -C /usr --strip-components=1 && \
	rm -rf julia-0.6.0-linux-x86_64.tar.gz && \
	julia -e 'Pkg.add("IJulia")'  && \
# Javascript
	wget https://nodejs.org/download/release/v4.8.2/node-v4.8.2-linux-x64.tar.gz && \
	tar xf node-v4.8.2-linux-x64.tar.gz -C /usr --strip-components=1 && \
	rm node-v4.8.2-linux-x64.tar.gz && \
	npm install -g ijavascript && \
	ijs --ijs-install-kernel && \
	rm -rf /usr/*.md && \
	rm -rf /usr/LICENSE && \
# Ruby
	gem install cztop iruby && \
	iruby register && \
# Fortran
	cd /root && \
	git clone https://github.com/ZedThree/jupyter-fortran-kernel.git && \
	pip3 install jupyter-fortran-kernel && \
	cd jupyter-fortran-kernel && \
	jupyter-kernelspec install fortran_spec/ && \
	cd /root && \
	rm -rf  jupyter-fortran-kernel && \
# Octave
	pip3 install octave_kernel && \
	python3 -m octave_kernel.install && \
# Prolog
	pip3 install --upgrade calysto_prolog && \
	python3 -m calysto_prolog install && \
# Haskell ( Not compliant with JupyterLab : if you use haskell , please click on " [Help] >  [Launch Classic Notebook]" in the browser )
	curl -sSL https://get.haskellstack.org/ | sh && \
	echo 'export PATH=/root/.local/bin:/root/.stack/programs/x86_64-linux/ghc-nopie-8.0.2/bin:$PATH' >> /etc/profile.d/haskell.sh && \
	. /etc/profile.d/haskell.sh && \
	cd /root && \
	git clone --depth 1 https://github.com/gibiansky/IHaskell.git && \
	cd IHaskell && \
	stack setup && \
	stack install --ghc-options=-O2 gtk2hs-buildtools && \
	stack install --ghc-options=-O2 && \
	ihaskell install --stack && \
	rm -rf /root/IHaskell && \
	rm -rf /root/.stack/indices/* && \
	rm -rf /root/.stack/programs/x86_64-linux/ghc-nopie-8.0.2.tar.xz && \
	rm -rf /tmp/*

EXPOSE	8888
CMD	["jupyter","lab"]
