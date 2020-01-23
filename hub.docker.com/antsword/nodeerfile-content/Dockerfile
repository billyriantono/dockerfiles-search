FROM andzuc/gentoo-armbuilder-s0

RUN time crossdev \
    --stable \
    --target "${TC_TARGET}" \
    --portage "-v" \
    --stage1
