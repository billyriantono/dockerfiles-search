FROM python:2.7-stretch

RUN wget https://github.com/progrium/entrykit/releases/download/v0.4.0/entrykit_0.4.0_Linux_x86_64.tgz && \
      tar xf entrykit_0.4.0_Linux_x86_64.tgz && \
      mv ./entrykit /usr/local/bin/. && \
      chmod +x /usr/local/bin/entrykit && \
      entrykit --symlink


RUN pip install --no-cache-dir uwsgi pipenv

CMD ["python2"]
