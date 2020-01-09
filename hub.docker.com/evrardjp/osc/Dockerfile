FROM opensuse/leap:15.1

RUN zypper ar https://download.opensuse.org/repositories/openSUSE:/Tools/openSUSE_15.1/openSUSE:Tools.repo \
    && zypper --gpg-auto-import-keys refresh \
    && zypper install --no-confirm --auto-agree-with-licenses --force-resolution --no-recommends osc lsb-release \
    && mkdir -p /root/.config/osc/

WORKDIR /workdir/

ENTRYPOINT ["osc"]
