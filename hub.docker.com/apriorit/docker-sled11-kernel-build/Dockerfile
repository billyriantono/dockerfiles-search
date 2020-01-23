FROM darksheer/sles11sp4
RUN zypper ar -f  http://ftp5.gwdg.de/pub/opensuse/discontinued/distribution/11.4/repo/oss/ oss-disc && \
    zypper --gpg-auto-import-keys --non-interactive install module-init-tools
