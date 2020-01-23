FROM rainbean/tensor:latest as builder
ADD . /src
WORKDIR /src
RUN python setup.py build_ext --inplace
RUN find mosaique \( -not -name __init__.py -not -name __main__.py -and -name \*.py -or -name \*.c \) -delete
RUN python setup.py bdist_wheel

FROM rainbean/tensor:latest
LABEL maintainer "Jimmy Lee"
WORKDIR /mnt
COPY --from=builder /src/dist/*.whl /mnt/
RUN pip install ./*.whl
ENTRYPOINT ["python", "-m", "mosaique"]
