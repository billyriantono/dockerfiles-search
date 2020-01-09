FROM tensorflow/tensorflow

MAINTAINER Hamid F.

#install prereqs
RUN apt-get update && apt-get install -y \
	libboost-all-dev \
	libmecab-dev \
	mecab \
	mecab-ipadic-utf8
	# python3-pip

#install Juman++
RUN curl -O http://lotus.kuee.kyoto-u.ac.jp/nl-resource/jumanpp/jumanpp-1.01.tar.xz && \
	tar xJvf jumanpp-1.01.tar.xz && \
	cd jumanpp-1.01 && \
	./configure && \
	make && \
	make install && \
	cd .. && \
	rm -R jumanpp-1.01 && \
	rm jumanpp-1.01.tar.xz

#install pyKNP, the juman++ python wrapper
RUN curl -O http://nlp.ist.i.kyoto-u.ac.jp/nl-resource/knp/pyknp-0.3.tar.gz && \
	tar xvf pyknp-0.3.tar.gz && \
	cd pyknp-0.3 && \
	python setup.py install	&& \
	cd .. && \
	rm -R pyknp-0.3 && \
	rm pyknp-0.3.tar.gz

#add pyKNP to iPython profile for sys.path
RUN ipython profile create && \
	echo "c.InteractiveShellApp.exec_lines = \
	['import sys; sys.path.append(\"/usr/local/lib/python2.7/dist-packages/pyknp-0.3-py2.7.egg\")']" \
	>> /root/.ipython/profile_default/ipython_kernel_config.py

#Enable javascript to run progress bar in Jupyter
RUN jupyter nbextension enable --py --sys-prefix widgetsnbextension

#install packages
RUN pip --no-cache-dir install tqdm \
	mecab-python3 \
	tinysegmenter3 \
	gensim

#install Python3 kernel on Jupyter
# RUN python3 -m pip install ipykernel

CMD ["/run_jupyter.sh", "--allow-root", "--NotebookApp.token=''"]