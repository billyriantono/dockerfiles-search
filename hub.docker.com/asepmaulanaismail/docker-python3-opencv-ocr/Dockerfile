FROM jjanzic/docker-python3-opencv
MAINTAINER Asep Maulana Ismail <asepmaulanaismail@gmail.com>

RUN apt-get update
RUN apt-get install -y python3-dev
RUN apt-get install -y libtesseract-dev libleptonica-dev
RUN apt-get update
RUN apt-get install -y autoconf-archive automake g++ libtool
RUN git clone https://github.com/tesseract-ocr/tesseract.git --branch 3.04 --single-branch tesseract-ocr 
RUN cd tesseract-ocr && ./autogen.sh && ./configure && make && make install && ldconfig
RUN pip install requests image tesserocr
RUN wget https://github.com/tesseract-ocr/tessdata/raw/master/eng.traineddata
RUN cp eng.traineddata /usr/local/share/tessdata/eng.traineddata
