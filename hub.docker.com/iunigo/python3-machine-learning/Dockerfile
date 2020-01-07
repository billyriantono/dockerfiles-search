FROM iunigo/alpine-python3

RUN apk add --update --no-cache \
    --virtual=.build-dependencies \
    git && \
    mkdir /src && \
    cd /src && \
    git clone --recursive -b v0.81 https://github.com/dmlc/xgboost && \
    sed -i '/#define DMLC_LOG_STACK_TRACE 1/d' /src/xgboost/dmlc-core/include/dmlc/base.h && \
    sed -i '/#define DMLC_LOG_STACK_TRACE 1/d' /src/xgboost/rabit/include/dmlc/base.h && \
    apk del .build-dependencies

RUN apk add --no-cache postgresql-libs && \
	apk add --no-cache \
        --virtual=.build-dependencies \
        g++ make gfortran file binutils \
        musl-dev python3-dev py-setuptools openblas-dev freetype-dev pkgconfig jpeg-dev zlib-dev postgresql-dev && \
    apk add libstdc++ openblas freetype && \
    \
    pip install numpy==1.16.3 && \
    pip install pandas==0.24.2 && \
    pip install scipy==1.2.1 && \
    pip install scikit-learn==0.20.3 && \
    pip install flask==1.0.2 && \
    pip install lifelines==0.21.1 && \
    pip install requests==2.21.0 && \
	pip install lime && \
	pip install sqlalchemy && \
	pip install psycopg2 && \
    pip install pandasql && \
    pip install statsmodels==0.9.0 && \
	ln -s locale.h /usr/include/xlocale.h && \
    cd /src/xgboost; make -j4 && \
    cd /src/xgboost/python-package && \
    python3 setup.py install && \
    rm /usr/include/xlocale.h && \
    \
    rm -r /root/.cache && \
    find /usr/lib/python3.*/ -name 'tests' -exec rm -r '{}' + && \
    find /usr/lib/python3.*/site-packages/ -name '*.so' -print -exec sh -c 'file "{}" | grep -q "not stripped" && strip -s "{}"' \; && \
    \
    apk del .build-dependencies