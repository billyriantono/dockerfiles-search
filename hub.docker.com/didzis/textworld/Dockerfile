FROM ubuntu:18.04

RUN apt update && apt install -y build-essential libffi-dev python3-dev python3-pip curl git

RUN pip3 install -U pip
RUN pip3 install ipython jupyter textworld chromedriver

RUN /bin/bash -c 'mkdir -p $(jupyter --data-dir)/nbextensions ;\
	cd $(jupyter --data-dir)/nbextensions\
	&& git clone https://github.com/lambdalisue/jupyter-vim-binding vim_binding\
	&& jupyter nbextension enable vim_binding/vim_binding'

WORKDIR /root/notebooks

ENTRYPOINT ["jupyter", "notebook", "--ip=0.0.0.0", "--no-browser", "--allow-root"]
