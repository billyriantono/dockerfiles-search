FROM pretix/standalone:stable
USER root
RUN pip3 install pretix-pages
RUN pip3 install pretix-sepadebit
RUN pip3 install pretix-passbook
RUN pip3 install pretix-cartshare
RUN pip3 install pretix-wirecard
RUN pip3 install pretix-fontpack-free
#RUN pip3 install pretix-stretchgoals
RUN pip3 install pretix-servicefees
RUN pip3 install pretix-newsletter-ml
RUN pip3 install pretix-fontpack-free
RUN pip3 install pretix-telephone

# Workaround: https://github.com/pc-coholic/pretix-cashpayment/issues/5#issuecomment-382447489
ENV DJANGO_SETTINGS_MODULE=
RUN pip3 install pretix-cashpayment
ENV DJANGO_SETTINGS_MODULE=production_settings

USER pretixuser
RUN cd /pretix/src && make production
