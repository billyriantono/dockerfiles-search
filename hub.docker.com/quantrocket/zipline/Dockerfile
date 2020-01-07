FROM quantrocket/anaconda3-uwsgi
MAINTAINER QuantRocket <support@quantrocket.com>

# Install ta-lib
RUN apt-get -y update && apt-get -y install \
    build-essential \
    libfreetype6-dev \
    libpng-dev \
    libopenblas-dev \
    liblapack-dev \
    gfortran \
    && cd /tmp \
    && curl --insecure -L http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz | tar xvz \
    && cd ta-lib \
    && ./configure --prefix=/usr \
    && make \
    && make install \
    && pip install TA-Lib==0.4.16 \
    && cd /tmp \
    && rm -r ta-lib

RUN /bin/bash -c "source activate /opt/conda" \
  && pip install https://codeload.github.com/quantrocket-llc/pyfolio/zip/qr0.9.0.8 \
  && pip install https://codeload.github.com/quantrocket-llc/zipline/zip/master \
  && pip install trading-calendars==1.1.0 \
  && pip install quantrocket-zipline-extensions \
  && pip install -U quantrocket-client \
  && /bin/bash -c "source deactivate"

COPY qrocket /tmp/uwsgi/qrocket
COPY uwsgi /etc/uwsgi

RUN mkdir -p /codeload \
  && mkdir -p /tmp/backtests \
  && /tmp/build.sh
