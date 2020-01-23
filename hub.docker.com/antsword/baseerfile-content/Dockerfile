FROM andzuc/gentoo-armbuilder

RUN time crossdev \
    --stable \
    --target "${TC_TARGET}" \
    --portage "-v" \
    --stage0
