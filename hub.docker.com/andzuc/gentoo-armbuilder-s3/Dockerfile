FROM andzuc/gentoo-armbuilder-s2

RUN time crossdev \
    --stable \
    --target "${TC_TARGET}" \
    --portage "-v" \
    --stage3
