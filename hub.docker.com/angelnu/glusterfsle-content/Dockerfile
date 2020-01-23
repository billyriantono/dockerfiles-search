FROM andzuc/gentoo-armbuilder-s1

RUN time crossdev \
    --stable \
    --target "${TC_TARGET}" \
    --portage "-v" \
    --stage2
