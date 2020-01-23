FROM flectrahq/flectra
USER root
#RUN  rm -rf ~/.cache/pip && rm -rf /tmp/*
#RUN mkdir /var/lib/flectra
# RUN set -x; echo deb http://ftp.debian.org/debian stretch-backports main > /etc/apt/sources.list.d/backports.list \
#         && apt-get update -qq \
#         && DEBIAN_FRONTEND=noninteractive apt-get install -yqq --no-install-recommends \
#             python3-paramiko \
#             python3-crypto \
#             python3-wheel \
#             python3-pil \
#             python3-lasso \
#             python3-watchdog \
#             python3-num2words \
#             python3-cffi \
#             python3-tz \
#             python3-unidecode \
#             python3-requests \
#             python3-numpy \
#             python3-dev \
#             build-essential \
#             libxmlsec1-dev \
#             xz-utils \
#     	    rsync \
#             unzip \
#             git \
#             uwsgi uwsgi-emperor uwsgi-plugin-python3 \
#         && rm -rf /var/lib/apt/lists/* && mkdir /var/lib/flectra/

# COPY ./flectra.conf /etc/flectra/
COPY ./addons /usr/lib/python3/dist-packages/flectra/addons/
#COPY --chown=flectra ./addons /usr/lib/python3/dist-packages/flectra/addons/

#RUN chown -R flectra /usr/lib/python3/dist-packages/flectra/addons/

USER flectra
ENTRYPOINT ["/entrypoint.sh"]
CMD ["flectra","-u","base,web,website,web_settings_dashboard,board"]


# #COPY ./tools/rename.py /rename.py
# #COPY ./entrypoint.sh /entrypoint.sh
# #ENTRYPOINT [ "/entrypoint.sh" ]
#USER flectra
# #CMD ["sh", '/entrypoint.sh']
# CMD ["flectra"]