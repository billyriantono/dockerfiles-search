FROM rainbean/tensor:latest as builder
ADD . /src
WORKDIR /src
RUN python setup.py bdist_wheel

FROM rainbean/tensor:latest
LABEL maintainer "Jimmy Lee"
WORKDIR /mnt
COPY --from=builder /src/dist/* .
RUN pip --no-cache-dir install ./*.whl
ENTRYPOINT ["python", "-m", "cell_morphology"]
