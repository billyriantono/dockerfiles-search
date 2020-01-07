FROM alpine:3.9.3 as builder

ARG GECKO_DRIVER_VERSION="v0.24.0"

RUN apk add --no-cache wget ca-certificates

# Create Robot work directory
RUN mkdir /robotframework \
          /robotframework/webdrivers \
          /robotframework/tests \
          /robotframework/output

# Copy files in image
COPY . /robotframework

# Download Mozilla WebDriver
RUN wget -nv -O /tmp/geckodriver-$GECKO_DRIVER_VERSION-linux64.tar.gz \
    https://github.com/mozilla/geckodriver/releases/download/$GECKO_DRIVER_VERSION/geckodriver-$GECKO_DRIVER_VERSION-linux64.tar.gz && \
    tar xzf /tmp/geckodriver-$GECKO_DRIVER_VERSION-linux64.tar.gz -C /robotframework/webdrivers && \
    rm /tmp/geckodriver-$GECKO_DRIVER_VERSION-linux64.tar.gz

# Creating main image
FROM alpine:3.9.3

LABEL IMAGE_NAME="docker-robotframework"
LABEL IMAGE_VERSION="v3.9.3"
LABEL BUILD_TIME="$(date '+%Y-%m-%d %H:%M:%S')"
LABEL DESCRIPTION="Docker image for Robot Framework with Selenium Library and Mozilla Webdriver"

ARG ROBOT_VERSION="3.1.1" 
ARG SELENIUM_LIBRARY_VERSION="3.3.1"
ARG FIREFOX_VERSION="60.6.1"

# Install Python 2.7, PyPi, Robot Framework with library
RUN set -xe && \
    apk update && \
    apk add --no-cache \
        curl ca-certificates python2 py2-pip openssh-client git \
        firefox-esr==$FIREFOX_VERSION-$(apk search firefox-esr | cut -d "-" -f 4) &&\
    pip install --disable-pip-version-check --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir \
    robotframework==$ROBOT_VERSION \
    robotframework-seleniumlibrary==$SELENIUM_LIBRARY_VERSION

# Robot variables
ENV PATH="/robotframework/webdrivers:${PATH}" \
    ROBOT_OPTIONS=""

# Copy files from temporary image
COPY --from=builder /robotframework /robotframework

WORKDIR /robotframework
VOLUME ["/robotframework/output", "/robotframework/tests"]

CMD ["./entrypoint.sh"]
