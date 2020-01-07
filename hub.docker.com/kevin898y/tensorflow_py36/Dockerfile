FROM kevin898y/tensorflow_py36:base 
MAINTAINER LAI

RUN pip3 --no-cache-dir install django \
	beautifulsoup4 \
	requests
RUN pip3 --no-cache-dir install nltk \
	gensim \
	https://download.pytorch.org/whl/cu100/torch-1.1.0-cp36-cp36m-linux_x86_64.whl\
	https://download.pytorch.org/whl/cu100/torchvision-0.3.0-cp36-cp36m-linux_x86_64.whl\
	transformers\
	git+https://github.com/boudinfl/pke.git