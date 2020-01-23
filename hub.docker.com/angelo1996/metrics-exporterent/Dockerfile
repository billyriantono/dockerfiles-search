FROM andzuc/gentoo-armbuilder-s4

# seed0: config
ENV TC_FEATURES="-sandbox -usersandbox buildpkg noman noinfo nodoc"
ENV TC_PROFILE=default/linux/arm/17.0/armv6j
RUN echo "ACCEPT_CHOSTS='${TC_TARGET}'" >>/etc/portage/make.conf \
    && sed -i \
	   's|PKGDIR=".*"|PKGDIR="'"/builder/packages"'"|' \
	   "/etc/portage/make.conf" \
    && sed -i \
	   's|PKGDIR=.*|PKGDIR="'"/builder/packages"'"|' \
	   "/usr/${TC_TARGET}/etc/portage/make.conf" \
    && sed -i \
	   's!ACCEPT_KEYWORDS="\(.*\)"!ACCEPT_KEYWORDS="'"\${ARCH}"'"!' \
	   "/usr/${TC_TARGET}/etc/portage/make.conf" \
    && sed -i \
	   's!FEATURES=".*"!FEATURES="'"${TC_FEATURES}"'"!' \
	   "/usr/${TC_TARGET}/etc/portage/make.conf" \
    && sed -i \
	   's!USE="\(.*\)"!USE="'"\1"'"!' \
	   "/usr/${TC_TARGET}/etc/portage/make.conf" \
    && cat "/usr/${TC_TARGET}/etc/portage/make.conf" \
    && ( ARCH=`PORTAGE_CONFIGROOT=/usr/${TC_TARGET}/ portageq envvar ARCH` \
	     PORTAGE_CONFIGROOT="/usr/${TC_TARGET}/" \
	     eselect profile set "${TC_PROFILE}"; eselect profile show ) \
    && mkdir -p /builder/seed \
    && mkdir -p /builder/packages

COPY portage "/usr/${TC_TARGET}/etc/portage"

# seed0: emerge base system 
# https://wiki.gentoo.org/wiki/Porting
ENV SEED_PKGLIST=" \
sys-devel/binutils \
sys-kernel/linux-headers \
sys-libs/glibc \
sys-devel/gcc \
net-misc/rsync \
net-misc/wget \
app-arch/tar \
app-arch/gzip \
app-arch/bzip2 \
sys-apps/baselayout \
sys-apps/coreutils \
sys-apps/findutils \
sys-apps/grep \
sys-apps/gawk \
sys-devel/patch \
sys-devel/make \
app-misc/pax-utils \
app-shells/bash \
dev-lang/python \
dev-vcs/git"
RUN time "${TC_TARGET}-emerge" -v --color n ${SEED_PKGLIST} \
    && emerge --root /builder/seed -v --color n --usepkgonly ${SEED_PKGLIST}

RUN time mkdir -p /builder/seed/etc/portage \
    && echo 'CHOST="'${TC_TARGET}'"' >>/builder/seed/etc/portage/make.conf \
    && grep "CFLAGS=" /usr/${TC_TARGET}/etc/portage/make.conf >>/builder/seed/etc/portage/make.conf \
    && grep "CXXFLAGS=" /usr/${TC_TARGET}/etc/portage/make.conf >>/builder/seed/etc/portage/make.conf \
    && cat /builder/seed/etc/portage/make.conf \
    && ln -s "../../usr/portage/profiles/${TC_PROFILE}" /builder/seed/etc/portage/make.profile

RUN mkdir -p /builder/ext/resin \
    && git clone https://github.com/balena-io-library/armv7hf-debian-qemu.git /builder/ext/resin \
    && ( export ARCH=`PORTAGE_CONFIGROOT=/usr/${TC_TARGET}/ portageq envvar ARCH`; \
	 sed -i 's!/usr/bin/qemu-.*-static!/emu/qemu-'"${ARCH}"'!' \
	     "/builder/ext/resin/resin-xbuild.go"; \
	 sed -i 's|"-execve", "-0"|"-execve", "/emu/qemu-'"${ARCH}"'", "-0"|' \
	     "/builder/ext/resin/resin-xbuild.go" ) \
    && ( cd /builder/ext/resin; ./build.sh )

COPY --from=andzuc/gentoo-armqemu /usr/bin/qemu-* /builder/ext/qemu/

# seed0: emerge stage1 gcc (C only)
# RUN time USE="nls nptl pch pie ssp -cilk -cxx -debug -doc -fortran -go -graphite -hardened -jit -libssp -mpx -multilib -objc -objc++ -objc-gc -openmp -pgo -regression-test -sanitize -vanilla -vtv" \
#     "${TC_TARGET}-emerge" -v --color n sys-devel/gcc \
#     && emerge --root /builder/seed -v --color n --usepkgonly sys-devel/gcc

#COPY builder /builder
#RUN time emerge -v dev-util/catalyst
#RUN catalyst -s "$(date +%Y.%m)"

# build @sysnodev
#RUN "${TC_TARGET}-emerge" --info
#RUN time "${TC_TARGET}-emerge" -ev --color n --keep-going @system --exclude "sys-devel/gcc"
