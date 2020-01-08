FROM ubuntu:18.04

# https://www.vivaolinux.com.br/dica/OCR-no-Ubuntu
# RUN sh -c 'echo "deb http://archive.ubuntu.com/ubuntu bionic universe" >> /etc/apt/sources.list'
RUN apt-get update
RUN apt-get install tesseract-ocr libtesseract-dev imagemagick -y

# https://stackoverflow.com/questions/14800730/tesseract-running-error
# RUN apt-get install wget -y
# RUN wget "https://github.com/tesseract-ocr/tessdata/raw/master/por.traineddata" -O "/usr/share/tesseract-ocr/4.00/tessdata/por.traineddata"
RUN apt-get install tesseract-ocr-por -y

# https://stackoverflow.com/questions/42928765/convertnot-authorized-aaaa-error-constitute-c-readimage-453
ADD ./ImageMagickPolicy/policy.xml /etc/ImageMagick-6

CMD [ "bash" ]