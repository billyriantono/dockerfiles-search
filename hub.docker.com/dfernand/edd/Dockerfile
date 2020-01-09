FROM python:2

RUN pip install Cython numpy pysam==0.11

# Install bedtools for pybedtools
ADD https://github.com/arq5x/bedtools2/releases/download/v2.28.0/bedtools-2.28.0.tar.gz /download/
RUN tar -zxvf download/bedtools-2.28.0.tar.gz; cd bedtools2; make; mv bin/* /usr/local/bin; cd ..; rm -r bedtools2

RUN pip install pybedtools edd
# ADD https://github.com/CollasLab/edd/archive/master.tar.gz .
# RUN tar -xvzf master.tar.gz -C .
# RUN cd edd-master/; python setup.py install

CMD [ "edd" ]
