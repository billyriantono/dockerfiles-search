# MIT License

# Copyright (c) 2017 Lihan Li

# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:

# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.

# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

FROM ubuntu:17.04
LABEL maintainer="Lihan Li <lilihan.it@gmail.com>"

RUN mkdir /data

EXPOSE 8888
WORKDIR /data
VOLUME ["/data"]

RUN apt-get -y update && \
    apt-get -y install build-essential && \
    apt-get -y install python3-pip \
                       cmake \
                       python-pip \
                       python-dev \
                       vim

RUN pip3 install \
        bokeh==0.12.13 \
        jupyter==1.0.0 \
        nltk==3.2.5 \
        numpy==1.13.3 \
        pytagcloud==0.3.5 \
        stop-words==2015.2.23.1 \
        wordcloud==1.3.1 \
        beautifulsoup4==4.5.1 \
        pandas \
        lightgbm \
        lightfm \
        requests \
        seaborn \
        scikit-learn \
        tensorflow

RUN python3 -m nltk.downloader -d /usr/local/share/nltk_data all

CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--allow-root", "--ip=0.0.0.0"]
