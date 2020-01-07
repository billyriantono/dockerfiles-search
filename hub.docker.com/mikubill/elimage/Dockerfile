FROM python:3.7.1-alpine
MAINTAINER billgm13@gmail.com

RUN mkdir elimage &&\
    cd elimage &&\
    mkdir data &&\
    mkdir templates &&\
    echo "import urllib.request" >> install.py &&\
    echo "url = \"https://github.com/Vim-cn/elimage/raw/master/main.py\"" >> install.py &&\
    echo "urllib.request.urlretrieve(url, \"main.py\")" >> install.py &&\
    echo "url = \"https://github.com/Vim-cn/elimage/raw/master/models.py\"" >> install.py &&\
    echo "urllib.request.urlretrieve(url, \"models.py\")" >> install.py &&\
    echo "url = \"https://github.com/Vim-cn/elimage/raw/master/config.py\"" >> install.py &&\
    echo "urllib.request.urlretrieve(url, \"config.py\")" >> install.py &&\
    echo "url = \"https://github.com/Vim-cn/elimage/raw/master/cloudflare.py\"" >> install.py &&\
    echo "urllib.request.urlretrieve(url, \"cloudflare.py\")" >> install.py &&\
    echo "url = \"https://github.com/Vim-cn/elimage/raw/master/elimage.sql\"" >> install.py &&\
    echo "urllib.request.urlretrieve(url, \"elimage.sql\")" >> install.py &&\
    python install.py &&\
    python -m pip install tornado filetype &&\
    chmod +x /elimage/* &&\
    sed -i 's/\/tmp/\/elimage\/data/g' /elimage/config.py 

WORKDIR /elimage
VOLUME /elimage/data

ENTRYPOINT /elimage/main.py
EXPOSE 8888
