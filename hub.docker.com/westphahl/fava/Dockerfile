FROM python:alpine as builder

RUN apk add --update libxml2-dev libxslt-dev gcc musl-dev g++
RUN pip install --install-option="--prefix=/install" fava==1.10

FROM python:alpine

COPY --from=builder /install /usr/local

ENV BEANCOUNT_FILE ""
ENV FAVA_OPTIONS ""
EXPOSE 5000
CMD fava --host 0.0.0.0 ${FAVA_OPTIONS} "${BEANCOUNT_FILE}"
