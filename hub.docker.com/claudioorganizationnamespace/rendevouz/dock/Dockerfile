FROM cl3m3nt/sphinx:latest
LABEL description "Sphinx build html watcher"

RUN pip install sphinx-autobuild

EXPOSE 8000

ENTRYPOINT ["sphinx-autobuild", "-H", "0.0.0.0"]
CMD ["/root/docs/source", "/root/docs/build"]
