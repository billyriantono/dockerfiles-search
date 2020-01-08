#tesseract stuff borrowed from vimagick/tesseract

FROM debian:jessie
RUN set -xe \
    && apt-get update \
    && apt-get install -y autoconf \
                          apt-utils \
                          build-essential \
                          curl \
                          git \
                          libcairo2 \
                          libcairo2-dev \
                          libgomp1 \
                          libicu52 \
                          libicu-dev \
                          liblept4 \
                          libleptonica-dev \
                          libopencv-dev \
                          libpango1.0-0 \
                          libpango1.0-dev \
                          libtool \
                          pkg-config \
                          python \
                          wget \
    && git clone https://github.com/tesseract-ocr/tesseract.git \
        && cd tesseract \
        && git checkout 3.04.01 \
        && ./autogen.sh \
        && ./configure \
        && make install \
        && cd .. \
    && rm -rf tesseract \
    && mkdir tessdata \
        && cd tessdata \
        && wget https://raw.githubusercontent.com/tesseract-ocr/tessdata/3.04.00/eng.cube.bigrams \
        && wget https://raw.githubusercontent.com/tesseract-ocr/tessdata/3.04.00/eng.cube.fold \
        && wget https://raw.githubusercontent.com/tesseract-ocr/tessdata/3.04.00/eng.cube.lm \
        && wget https://raw.githubusercontent.com/tesseract-ocr/tessdata/3.04.00/eng.cube.nn \
        && wget https://raw.githubusercontent.com/tesseract-ocr/tessdata/3.04.00/eng.cube.params \
        && wget https://raw.githubusercontent.com/tesseract-ocr/tessdata/3.04.00/eng.cube.size \
        && wget https://raw.githubusercontent.com/tesseract-ocr/tessdata/3.04.00/eng.cube.word-freq \
        && wget https://raw.githubusercontent.com/tesseract-ocr/tessdata/3.04.00/eng.tesseract_cube.nn \
        && wget https://raw.githubusercontent.com/tesseract-ocr/tessdata/3.04.00/eng.traineddata \
        && mv * /usr/local/share/tessdata/ \
        && cd .. \
    && rm -rf tessdata /var/cache/apk/* \
    && curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.1/install.sh | bash \
    && echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.bashrc \
    && echo '[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"' >> ~/.bashrc \
    && . ~/.bashrc \
    && nvm install 8 \
    && mkdir dv_install \
    && npm install -g node-gyp \

#ENTRYPOINT ["tesseract"]
#CMD ["-h"]
