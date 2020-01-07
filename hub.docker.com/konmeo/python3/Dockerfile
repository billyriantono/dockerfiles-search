FROM konmeo/minideb

MAINTAINER konmeo

ENV LANG C.UTF-8

RUN install_packages libexpat1 libffi6 libgdbm3 libmpdec2 \
        libreadline7 libsqlite3-0 libssl1.1 zlib1g

COPY --from=konmeo/python3-build /usr/local/lib2 /usr/local/lib/
COPY --from=konmeo/python3-build /usr/local/bin /usr/local/bin/

RUN ldconfig && \
    python3 --version && \
    python3 -m test.pystone

ENV PYTHON_PIP_VERSION 9.0.1

RUN install_packages wget && \
    wget -q https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py --disable-pip-version-check \
        --no-cache-dir "pip==$PYTHON_PIP_VERSION" && \
    \
    apt-get purge -y --auto-remove wget && \
    rm -f get-pip.py && \
    \
    pip3 --version

RUN echo "[list]\nformat=legacy" > /etc/pip.conf

CMD ["python3", "--version"]
