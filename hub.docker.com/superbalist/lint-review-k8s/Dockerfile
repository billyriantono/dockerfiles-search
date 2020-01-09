FROM python:3.7

ARG BUILD_DATE
ARG VCS_REF
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="lint-review-k8s" \
      org.label-schema.description="Lint reviewer running on Kubnernetes" \
      org.label-schema.url="https://github.com/Superbalist/lint-review-k8s" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/Superbalist/lint-review-k8s" \
      org.label-schema.vendor="superbalist" \
      org.label-schema.schema-version="1.0.0"

ENV PYTHONUNBUFFERED 1
ENV PYTHONPATH $PYTHONPATH:/usr/src/app/

WORKDIR /usr/src/app/
COPY entrypoint.sh entrypoint.sh
COPY gunicorn.conf.py gunicorn.conf.py
COPY lintreview /usr/src/app/lintreview
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

ENTRYPOINT ["./entrypoint.sh"]
CMD ["gunicorn", "-c", "/usr/src/app/gunicorn.conf.py", "lintreview.wsgi:app"]
