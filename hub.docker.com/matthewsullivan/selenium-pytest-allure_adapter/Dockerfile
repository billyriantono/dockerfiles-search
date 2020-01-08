FROM alpine:latest

ENV pytest_version=4.0.1 \
    allure_version=2.5.4 \
    pytest_forked=0.2 \
    pytest_xdist=1.24.1 \
    pytest_rerun=6.0 \
    selenium_version=3.141.0 \
    PyYAML_version=3.13 \
    chromedriver_version=73.0.3683.20

RUN apk add --no-cache unzip chromium chromium-chromedriver python3-dev \
    && pip3 install --no-cache-dir allure-pytest==$allure_version \
    allure-python-commons==$allure_version pytest==$pytest_version \
    pytest-forked==$pytest_forked pytest-xdist==$pytest_xdist \
    pytest-rerunfailures==$pytest_rerun \ 
    selenium==$selenium_version PyYAML==$PyYAML_version \
    && wget -q "https://chromedriver.storage.googleapis.com/$chromedriver_version/chromedriver_linux64.zip" -O /tmp/chromedriver.zip \
    && unzip /tmp/chromedriver.zip -d . \
    && rm /tmp/chromedriver.zip \
    && chmod u+x chromedriver \
    && apk del unzip

ENV PATH="/chromedriver:${PATH}"
