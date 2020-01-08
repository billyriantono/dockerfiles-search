FROM konmeo/quant

EXPOSE 5000

USER root
RUN install_packages libxslt1.1
RUN pip3 install --no-cache-dir -f https://konmeo.github.io/wheelhouse/ \
    uwsgi
RUN pip3 install --no-cache-dir \
        flask flask-appconfig flask-restplus \
        requests lxml pyyaml hvac apscheduler

USER user
