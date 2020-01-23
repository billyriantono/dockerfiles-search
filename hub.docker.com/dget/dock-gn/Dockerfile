FROM dget/dock-gn:1804

RUN pip install --no-cache-dir jupyter

RUN mkdir /.local && chmod a+rwx /.local

WORKDIR /workdir

EXPOSE 8888

ENTRYPOINT ["/entry.sh"]

CMD ["bash", "-c", "jupyter notebook \
        --notebook-dir=/workdir \
        --ip 0.0.0.0 \
        --no-browser \
        --allow-root"]
