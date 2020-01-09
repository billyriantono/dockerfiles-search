FROM nsml/default_ml:tf-1.4.1

RUN apt-get update
RUN apt-get install wget
#RUN wget https://s3-us-west-1.amazonaws.com/fasttext-vectors/word-vectors-v2/cc.ko.300.bin.gz
#RUN gzip -d cc.ko.300.bin.gz
RUN wget https://www.dropbox.com/s/qxhcn6xd0y5iz00/cc.ko.300.vec?dl=1 -O cc.ko.300.vec
RUN pip3 install gensim

