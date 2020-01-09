FROM konmeo/scipy

COPY lib/libta_lib.so.0.4.0 /usr/lib/libta_lib.so

RUN pip3 install --no-cache-dir -f https://konmeo.github.io/wheelhouse/ \
    bottleneck TA-Lib

RUN pip3 install --no-cache-dir \
    pandas-datareader quandl backtrader cufflinks \
    pandas_market_calendars pyfolio pymarketstore

RUN export BRANCH=develop && \
    install_packages wget unzip && \
    wget https://github.com/konmeo/backtrader_plotting/archive/$BRANCH.zip && \
    unzip $BRANCH.zip && \
    cd backtrader_plotting-$BRANCH && \
    pip3 install --no-binary :all: . && \
    cd .. && \
    rm -rf $BRANCH.zip backtrader_plotting-$BRANCH && \
    apt-get purge --autoremove -y wget unzip
