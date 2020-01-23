FROM gitea/gitea
LABEL maintainer="Abhinav A V<abhai2k@gmail.com>"

RUN apk --no-cache add asciidoctor freetype freetype-dev gcc g++ libpng python-dev py-pip python3-dev py3-pip linux-headers zeromq-dev
# install any other package you need for your external renderers

RUN pip3 install --upgrade pip
RUN pip3 install -U setuptools
RUN pip3 install jupyter matplotlib docutils 
# add above any other python package you may need to install
