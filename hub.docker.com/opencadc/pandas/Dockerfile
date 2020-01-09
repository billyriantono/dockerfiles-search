FROM opencadc/astropy:3.5-alpine

RUN apk --no-cache add g++

RUN pip --no-cache-dir install cython \
    && pip --no-cache-dir install pandas

RUN apk --no-cache del g++
