# Tag: bildcode/pyside:latest

# debian with latest Python 2.7 release
FROM python:2.7-slim-stretch

# install Qt / Pyside / CI-helper modules
RUN apt-get update && \
    apt-get autoclean && \
    apt-get install -y --no-install-recommends \
        libqt4-dev \
        cmake \
        build-essential \
        xvfb \
        libegl1-mesa \
        x11-xserver-utils \
        libxkbcommon-x11-0 \
        x11-utils && \
    apt-get clean && \
    rm -rf /var/cache/apk/* && \
    python -m pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir \
        anybadge \
        devpi-client \
        flake8 \
        pylint \
        pyside \
        pytest==4.6.4 \
        pytest-cov \
        pytest-qt \
        pytest-xvfb \
        Qt.py \
        xvfbwrapper && \
    apt-get purge -y build-essential && \
    apt-get purge -y cmake

# setup virtual display
ENV DISPLAY=:99
ENV SCREEN=0
ENV DBUS_SESSION_BUS_ADDRESS=/dev/null

# turn this on for verbose qt feedback
ENV QT_DEBUG_PLUGINS=0

# start the container with a bash shell by default
CMD ["bin/bash"]
