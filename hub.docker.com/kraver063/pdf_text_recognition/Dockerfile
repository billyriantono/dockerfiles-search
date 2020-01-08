#FROM tiangolo/uwsgi-nginx-flask:python3.6-alpine3.7
FROM jjanzic/docker-python3-opencv

RUN apt-get -y install ghostscript tesseract-ocr
RUN pip install flask

RUN pip install pyocr
RUN pip install wand
RUN pip install PyPDF2
RUN pip install APScheduler
RUN pip install opencv-contrib-python

RUN mkdir /tmp/uploads
RUN mkdir /tmp/content

RUN mkdir /app
WORKDIR /app


RUN echo "Europe/Brussels" >  /etc/timezone
ENV FLASK_APP=/app/main.py
EXPOSE 80

CMD python -m flask run --host=0.0.0.0 --port=80
COPY *.py /app

#ENV TESSDATA https://raw.githubusercontent.com/tesseract-ocr/tessdata/master/eng.traineddata
#ENV OPENCV https://github.com/opencv/opencv/archive/3.3.0.tar.gz
#ENV OPENCV_VER 3.3.0
#ENV CC /usr/bin/clang
#ENV CXX /usr/bin/clang++

#RUN apk add -U --no-cache --virtual=build-dependencies \
#    linux-headers musl libxml2-dev libxslt-dev libffi-dev g++ \
#    musl-dev libgcc openssl-dev jpeg-dev zlib-dev freetype-dev build-base \
#    lcms2-dev openjpeg-dev python3-dev make cmake clang clang-dev ninja \
#
#    && apk add --no-cache gcc tesseract-ocr zlib jpeg libjpeg freetype openjpeg curl python3 \
#    && curl https://bootstrap.pypa.io/get-pip.py | python3 \
#    && ln -s /usr/bin/python3 /usr/bin/python \
#    && ln -s /usr/bin/pip3 /usr/bin/pip \
#    && curl $TESSDATA -o /usr/share/tessdata/eng.traineddata \
#    && ln -s /usr/include/locale.h /usr/include/xlocale.h \
#    && pip install -U --no-cache-dir Pillow pytesseract numpy

#RUN apk add --no-cache curl cmake clang-dev ninja
#
#RUN mkdir /opt && cd /opt && \
#    curl -L $OPENCV | tar zx && \
#    cd opencv-$OPENCV_VER && \
#    mkdir build && cd build && \
#    cmake -G Ninja \
#          -D CMAKE_BUILD_TYPE=RELEASE \
#          -D CMAKE_INSTALL_PREFIX=/usr/local \
#          -D WITH_FFMPEG=NO \
#          -D WITH_IPP=NO \
#          -D PYTHON_EXECUTABLE=/usr/bin/python \
#          -D WITH_OPENEXR=NO .. && \
#    ninja && ninja install && \
#    ln -s /usr/local/lib/python3.6/site-packages/cv2.cpython-36m-x86_64-linux-gnu.so \
#          /usr/lib/python3.6/site-packages/cv2.so && \
#    apk del build-dependencies && \
#    rm -rf /var/cache/apk/*

