FROM homeassistant/home-assistant:0.72.0

RUN set -e && \
    cd /tmp && \
    apt-get -y update && \
    apt-get -y install git && \
    git clone https://github.com/ryanwinter/open-zwave.git && \
    export LOCAL_OPENZWAVE=/tmp/open-zwave && \
    pip3 uninstall -y python-openzwave && \
    pip3 install --no-cache-dir 'python_openzwave==0.4.3' --install-option="--flavor=dev" && \

    # Cleanup
    apt-get remove -y --purge git && \
    apt-get -y --purge autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/src/app/build/
