FROM darkmagician/python3

COPY sources.list.cn /etc/apt/sources.list
RUN apt-get update

RUN apt-get -y install python3-urllib3='1.12-1~bpo8+1' python3-requests='2.8.1-1~bpo8+1' 
RUN apt-get -y install zlib1g-dev libjpeg-dev tesseract-ocr tesseract-ocr-eng
RUN apt-get clean

RUN pip3 install Pillow
RUN pip3 install pytesseract
RUN pip3 install sqlalchemy
RUN TABULATE_INSTALL=lib-only;pip3 install tabulate

RUN wget http://myquant.cn/downloads/sdk/python/gmsdk-2.7.0-py3-x64-linux.zip
RUN unzip gmsdk-2.7.0-py3-x64-linux.zip
RUN pip3 install /gmsdk-2.7.0-py3-x64-linux/gmsdk-2.7.0-py3-none-any.whl
RUN rm /gmsdk-2.7.0-py3-x64-linux.zip

RUN echo "export PYTHONIOENCODING=UTF-8;" >> /home/admin/.profile
RUN echo "TZ='Asia/Shanghai'; export TZ;" >> /home/admin/.profile
RUN echo "TESSDATA_PREFIX='/usr/share/tesseract-ocr/tessdata'; export TESSDATA_PREFIX;" >> /home/admin/.profile
RUN echo export PATH="~:$PATH" >> /home/admin/.profile








