FROM floydhub/pytorch:0.3.0-gpu.cuda8cudnn6-py3.24

RUN apt-get install wget unzip
RUN wget https://github.com/facebookresearch/fastText/archive/v0.1.0.zip
RUN unzip v0.1.0.zip
WORKDIR /fastText-0.1.0
RUN make

RUN wget https://s3-us-west-1.amazonaws.com/fasttext-vectors/wiki.ko.zip
RUN unzip wiki.ko.zip

RUN apt-get install libicu-dev
RUN pip3 install polyglot
RUN pip3 install gensim
