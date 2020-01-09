    
FROM lambci/lambda:build-python3.7

RUN python -m pip install --upgrade pip \
    && python -m pip install --upgrade setuptools \
    && python -m pip install mysql-connector-python \
    && python -m pip install pycryptodome \
    && python -m pip install pycrypto
