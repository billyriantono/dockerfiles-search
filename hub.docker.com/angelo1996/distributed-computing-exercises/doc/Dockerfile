FROM andzuc/gentoo-armbuilder-s3

RUN time crossdev \
    --stable \
    --target "${TC_TARGET}" \
    --portage "-v" \
    --stage4
