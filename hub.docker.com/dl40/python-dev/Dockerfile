#docker build -t soclepythonalpine:latest .

#docker run -it --rm --name py -v /home/tux/dev/ml40/py/:/home/devtux/repogit soclepythonalpine bash 

#docker run -it --rm --name py -v /home/tux/dev/ml40/py/:/home/devtux/repogit soclepythonalpine sh 


FROM python:3.6-alpine


#Mise en place d'un volume de partage pour les datas produites
####### LOCAL USER SETTING ########
ARG user=devtux
ARG group=devtux
# Verify whether this uid exists already at hosts
ARG uid=1000
ARG gid=1000
#RUN addgroup -g ${gid} ${group} \
#    && adduser -h "/home/devtux" -u ${uid} -G root -s /bin/bash ${user}
RUN addgroup -g ${gid} -S ${group} \
     && adduser -h "/home/devtux" -u ${uid} -D -G root -s /bin/bash ${user} \
     && mkdir /home/devtux/data \
     && mkdir /home/devtux/repogit

VOLUME "/home/devtux/data"

##Mise en place d'un volume de partage pour les sources
VOLUME "/home/devtux/repogit"
WORKDIR "/home/devtux/repogit"


#RUN apk add --update --no-cache bash \
RUN apk add --update --virtual .build-deps curl gcc g++ make \
    && rm -rf /var/cache/apk/* \
#install de talib
    && mkdir /home/devtux/talib
#RUN wget http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz -O ta-lib-0.4.0-src.tar.gz
COPY ./containerfiles/ta-lib-0.4.0-src.tar.gz /home/devtux/talib/
RUN cd /home/devtux/talib/ \
    && tar -xvzf ta-lib-0.4.0-src.tar.gz \
    # Compilation
    && cd /home/devtux/talib/ta-lib \
    && ./configure --prefix=/usr \
    && make \
    && make install \
    && make clean




##compil des librairies python
RUN ln -s /usr/include/locale.h /usr/include/xlocale.h \
    && pip install numpy==1.13.* \
    && pip install TA-Lib==0.4.* \
    && pip install pandas==0.20.* \
    && pip install pandas-datareader==0.4.* \
    && pip install HermesCache==0.6.* \
    && pip install var_dump==1.1.* \
    && pip install pytest==3.2.* \
    && pip install pybuilder==0.11.* \
    && pip install flake8==3.4.* \
    && pip install memory_profiler==0.47 \
    && pip install line_profiler==2.0 \

#Install celery
    && pip install Celery==4.1.* \
    && pip install pyinotify==0.9.* \
    && pip install flower==0.9.* \

    && pip install redis==2.10.*

#Install Numba
#RUN pip install -i https://pypi.anaconda.org/sklam/simple llvmlite \
#    && pip install numba==0.34.* \ 

#ENV PATH=/opt/conda/bin:$PATH \ 
#    MINICONDA=Miniconda3-4.3.27.1-Linux-x86_64.sh
#RUN apk add --no-cache --virtual=build-deps --update-cache \ 
#    wget bash  
#RUN wget -q https://repo.continuum.io/miniconda/Miniconda3-4.3.27.1-Linux-x86_64.sh  
#RUN /bin/sh Miniconda3-4.3.27.1-Linux-x86_64.sh -b -p /opt/conda  
#RUN rm -rf /root/.continuum /opt/conda/pkgs/* \
#    && rm Miniconda3-4.3.27.1-Linux-x86_64.sh \
#    && apk del build-deps 


#RUN conda install numba



#pour celery : a virer a l'occasion car normelement on ne doit pas lancer celery en root
#ENV C_FORCE_ROOT "true"
EXPOSE 5555



#RUN apk --update --no-cache add py2-pip ca-certificates musl-dev musl-utils musl-dbg gcc libevent-dev python2-dev \
#  libxml2-dev libxslt-dev libffi-dev openssl-dev
#RUN pip install --no-cache-dir --upgrade pip
#RUN cp -r /usr/include/libxml2/libxml/ /usr/include
#RUN pip install --no-cache-dir scrapy scrapyd
#RUN pip install --no-cache-dir Scrapy==1.4.* 


RUN apk add --no-cache gcc musl-dev openssl-dev libxml2-dev libxslt-dev libffi-dev libxml2 libxslt \
    && pip install scrapy \
    && apk del gcc musl-dev openssl-dev libxml2-dev libxslt-dev libffi-dev



####Nettoyage
RUN rm -rf /var/cache/apk/* \
    && rm -rf ~/.cache/pip/ \
    && find /usr/local \( -type d -a -name test -o -name tests \) -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \)  -exec rm -rf '{}' + \
    && runDeps="$( \
        scanelf --needed --nobanner --recursive /usr/local \
                | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
                | sort -u \
                | xargs -r apk info --installed \
                | sort -u \
    )" \
    && apk add --virtual .rundeps $runDeps \
## !!!!!!!! a voir si la ligne suivante ne pose pas de prb pour compiler à la volée avec numba
#    && apk del .build-deps \
    && rm -rf /home/devtux/talib/



#ENV PYTHONPATH $PYTHONPATH:/home/devtux/repogit/reponsed/py/ml40/src/main/python:/home/tux/dev/reponsed/py/ml40/src/unittest/python
#ENV PYTHONPATH $PYTHONPATH:/home/devtux/repogit/reponsed/py/ml40/src/main/scripts:
#WORKDIR "/home/devtux/repogit/reponsed/py/ml40/src/main/scripts"

#USER devtux

CMD ["sh"]

