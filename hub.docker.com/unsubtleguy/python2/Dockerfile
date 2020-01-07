FROM bitnami/minideb:stretch

RUN install_packages build-essential libssl-dev libffi-dev python-dev python-pip python-setuptools python-wheel -y
RUN pip install twisted \
        w3lib \
        lxml \
        parsel \
        functools32 \
        cssselect \
        pydispatcher \
        pyopenssl \
        cryptography \
        scrapy \
        ScrapyElasticSearch \
        cffi \
        enum34 \
        ndg-httpsclient

CMD ["python"]
