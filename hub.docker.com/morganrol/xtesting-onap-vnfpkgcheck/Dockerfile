FROM opnfv/xtesting

ARG ONAP_TAG=master

COPY thirdparty-requirements.txt thirdparty-requirements.txt

RUN apk --no-cache add --virtual .build-deps --update \
        python-dev build-base linux-headers libffi-dev \
        openssl-dev libjpeg-turbo-dev && \
    git clone --depth 1 https://git.onap.org/demo -b $ONAP_TAG /src/demo && \
    git clone --depth 1 https://git.onap.org/vvp/validation-scripts -b $ONAP_TAG /src/valid_script && \
    pip install \
        -rthirdparty-requirements.txt && \
    rm -r thirdparty-requirements.txt && \
    apk del .build-deps

COPY testcases.yaml /usr/lib/python2.7/site-packages/xtesting/ci/testcases.yaml
CMD ["run_tests", "-t", "all"]
