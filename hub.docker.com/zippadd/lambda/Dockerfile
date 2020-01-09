FROM lambci/lambda:provided

FROM zippadd/lambda-base-2

RUN curl https://lambci.s3.amazonaws.com/fs/nodejs10.x.tgz | tar -zx -C /

ENV PATH=/var/lang/bin:$PATH \
    LD_LIBRARY_PATH=/var/lang/lib:$LD_LIBRARY_PATH \
    AWS_EXECUTION_ENV=AWS_Lambda_nodejs10.x

COPY --from=0 /var/runtime/init /var/rapid/init

ENTRYPOINT ["/var/rapid/init", "--bootstrap", "/var/runtime/bootstrap"]
