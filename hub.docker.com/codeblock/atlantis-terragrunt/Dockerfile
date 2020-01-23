FROM runatlantis/atlantis:v0.8.1

RUN apk -v --update add \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        && \
    pip install --upgrade awscli==1.14.5 s3cmd==2.0.1 python-magic && \
    apk -v --purge del py-pip && \
    rm /var/cache/apk/*
ADD https://github.com/gruntwork-io/terragrunt/releases/download/v0.18.7/terragrunt_linux_amd64 /bin/terragrunt-binary
ADD terragrunt /bin/terragrunt
RUN chmod 755 /bin/terragrunt-binary
RUN chmod 755 /bin/terragrunt
