FROM python:3.4-onbuild

EXPOSE 8000

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["gunicorn", "-b", "0.0.0.0:8000", "-c", "config/gunicorn.py", "mooq.wsgi"]
