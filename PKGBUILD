# AArch64 multi-platform
# Maintainer: Kevin Mihelich <kevin@archlinuxarm.org>

buildarch=8

pkgbase=linux-aarch64
_srcname=linux-5.1
_kernelname=${pkgbase#linux}
_desc="AArch64 multi-platform"
pkgver=5.1.15
pkgrel=1
arch=('aarch64')
url="http://www.kernel.org/"
license=('GPL2')
makedepends=('xmlto' 'docbook-xsl' 'kmod' 'inetutils' 'bc' 'git' 'uboot-tools' 'vboot-utils' 'dtc')
options=('!strip')
source=("http://www.kernel.org/pub/linux/kernel/v5.x/${_srcname}.tar.xz"
        "http://www.kernel.org/pub/linux/kernel/v5.x/patch-${pkgver}.xz"
        '0001-net-smsc95xx-Allow-mac-address-to-be-set-as-a-parame.patch'
        '0002-arm64-dts-rockchip-disable-pwm0-on-rk3399-firefly.patch'
        '0003-arm64-dts-rockchip-add-usb3-controller-node-for-RK33.patch'
        '0004-arm64-dts-rockchip-enable-usb3-nodes-on-rk3328-rock6.patch'
        '0005-arm64-dts-rockchip-improve-rk3328-roc-cc-rgmii-perfo.patch'
        '0006-arm64-dts-rockchip-enable-usb3-nodes-on-roc-rk3328-c.patch'
        '0007-arm64-dts-rockchip-make-USB2.0-port-works-on-host-mo.patch'
        '0008-arm64-dts-rockchip-enable-display-nodes-on-rk3328-ro.patch'
        '0009-arm64-dts-rockchip-give-some-life-to-the-rk3328-roc-.patch'
        '0010-arm64-dts-rockchip-add-more-cpu-operating-points-for.patch'
        '0011-arm64-dts-rockchip-add-rk3328-roc-cc-cpu-supply-entr.patch'
        '0012-arm64-dts-rockchip-eMMC-additions-for-rk3328-roc-cc.patch'
        '0013-arm64-dts-rockchip-enable-HDMI-CEC-on-rk3328.patch'
        '0014-arm64-dts-rockchip-add-spdif-sound-hdmi-audio-on-roc.patch'
	'0015-arm64-dts-rockchip-add-sound-dai-cells-to-HDMI-of-rk.patch'
        'config'
        'linux.preset'
        '60-linux.hook'
        '90-linux.hook')
md5sums=('15fbdff95ff98483069ac6e215b9f4f9'
         'aed4686410e23561f67f5c512d0a6245'
         '2702c4bb01bef91b519a89c6c241340a'
         '9ed275df0ce4ca1e5c68b5cfc45257bb'
         '07ec98955a7243fdbfdb1e58561a18f0'
         '751854084c81a3c05607e227f2c3349c'
         '2ac66b3ba77a3e0efc62f33274655841'
         'd3b22f26eb641e868e794c92332c6fd3'
         'b31a2fd3fdda073ee1ca9de97273fcea'
         '2e6d8431d079e3b1c6e665df867ecaff'
         '3614fee91a5d3dd1ce1440fb7f1c207d'
         '554132a0e76c8af0e204980dd2692baa'
         '322be6b1c03981e6ba7d0d99d1af6684'
         '199e30bc476ddde56e9861138321b2b9'
         'd6dc74b9b4e9ba9af936adb27605d160'
         '2e98b40f95ea6e6a63ba1df3e95b9ae1'
         '831555cc1dd3a77096faae6be1f52d51'
         'f44f3e8ef7f77322c7bf268af950eef4'
         '41cb5fef62715ead2dd109dbea8413d6'
         'ce6c81ad1ad1f8b333fd6077d47abdaf'
         '3dc88030a8f2f5a5f97266d99b149f77')

prepare() {
  cd ${_srcname}

  # add upstream patch
  git apply --whitespace=nowarn ../patch-${pkgver}

  # ALARM patches
  git apply ../0001-net-smsc95xx-Allow-mac-address-to-be-set-as-a-parame.patch
  git apply ../0002-arm64-dts-rockchip-disable-pwm0-on-rk3399-firefly.patch
  git apply ../0003-arm64-dts-rockchip-add-usb3-controller-node-for-RK33.patch
  git apply ../0004-arm64-dts-rockchip-enable-usb3-nodes-on-rk3328-rock6.patch
  git apply ../0005-arm64-dts-rockchip-improve-rk3328-roc-cc-rgmii-perfo.patch
  git apply ../0006-arm64-dts-rockchip-enable-usb3-nodes-on-roc-rk3328-c.patch
  git apply ../0007-arm64-dts-rockchip-make-USB2.0-port-works-on-host-mo.patch
  git apply ../0008-arm64-dts-rockchip-enable-display-nodes-on-rk3328-ro.patch
  git apply ../0009-arm64-dts-rockchip-give-some-life-to-the-rk3328-roc-.patch
  git apply ../0010-arm64-dts-rockchip-add-more-cpu-operating-points-for.patch
  git apply ../0011-arm64-dts-rockchip-add-rk3328-roc-cc-cpu-supply-entr.patch
  git apply ../0012-arm64-dts-rockchip-eMMC-additions-for-rk3328-roc-cc.patch
  git apply ../0013-arm64-dts-rockchip-enable-HDMI-CEC-on-rk3328.patch
  git apply ../0014-arm64-dts-rockchip-add-spdif-sound-hdmi-audio-on-roc.patch
  git apply ../0015-arm64-dts-rockchip-add-sound-dai-cells-to-HDMI-of-rk.patch

  cat "${srcdir}/config" > ./.config

  # add pkgrel to extraversion
  sed -ri "s|^(EXTRAVERSION =)(.*)|\1 \2-${pkgrel}|" Makefile

  # don't run depmod on 'make install'. We'll do this ourselves in packaging
  sed -i '2iexit 0' scripts/depmod.sh
}

build() {
  cd ${_srcname}

  # get kernel version
  make prepare

  # load configuration
  # Configure the kernel. Replace the line below with one of your choice.
  #make menuconfig # CLI menu for configuration
  #make nconfig # new CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config

  # Copy back our configuration (use with new kernel version)
  #cp ./.config ../${pkgbase}.config

  ####################
  # stop here
  # this is useful to configure the kernel
  #msg "Stopping build"
  #return 1
  ####################

  #yes "" | make config

  # build!
  unset LDFLAGS
  make ${MAKEFLAGS} Image Image.gz modules
  # Generate device tree blobs with symbols to support applying device tree overlays in U-Boot
  make ${MAKEFLAGS} DTC_FLAGS="-@" dtbs
}

_package() {
  pkgdesc="The Linux Kernel and modules - ${_desc}"
  depends=('coreutils' 'linux-firmware' 'kmod' 'mkinitcpio>=0.7')
  optdepends=('crda: to set the correct wireless channels of your country')
  provides=('kernel26' "linux=${pkgver}")
  replaces=('linux-armv8')
  conflicts=('linux')
  backup=("etc/mkinitcpio.d/${pkgbase}.preset")
  install=${pkgname}.install

  cd ${_srcname}

  KARCH=arm64

  # get kernel version
  _kernver="$(make kernelrelease)"
  _basekernel=${_kernver%%-*}
  _basekernel=${_basekernel%.*}

  mkdir -p "${pkgdir}"/{boot,usr/lib/modules}
  make INSTALL_MOD_PATH="${pkgdir}/usr" modules_install
  make INSTALL_DTBS_PATH="${pkgdir}/boot/dtbs" dtbs_install
  cp arch/$KARCH/boot/Image{,.gz} "${pkgdir}/boot"

  # make room for external modules
  local _extramodules="extramodules-${_basekernel}${_kernelname}"
  ln -s "../${_extramodules}" "${pkgdir}/usr/lib/modules/${_kernver}/extramodules"

  # add real version for building modules and running depmod from hook
  echo "${_kernver}" |
    install -Dm644 /dev/stdin "${pkgdir}/usr/lib/modules/${_extramodules}/version"

  # remove build and source links
  rm "${pkgdir}"/usr/lib/modules/${_kernver}/{source,build}

  # now we call depmod...
  depmod -b "${pkgdir}/usr" -F System.map "${_kernver}"

  # add vmlinux
  install -Dt "${pkgdir}/usr/lib/modules/${_kernver}/build" -m644 vmlinux

  # sed expression for following substitutions
  local _subst="
    s|%PKGBASE%|${pkgbase}|g
    s|%KERNVER%|${_kernver}|g
    s|%EXTRAMODULES%|${_extramodules}|g
  "

  # install mkinitcpio preset file
  sed "${_subst}" ../linux.preset |
    install -Dm644 /dev/stdin "${pkgdir}/etc/mkinitcpio.d/${pkgbase}.preset"

  # install pacman hooks
  sed "${_subst}" ../60-linux.hook |
    install -Dm644 /dev/stdin "${pkgdir}/usr/share/libalpm/hooks/60-${pkgbase}.hook"
  sed "${_subst}" ../90-linux.hook |
    install -Dm644 /dev/stdin "${pkgdir}/usr/share/libalpm/hooks/90-${pkgbase}.hook"
}

_package-headers() {
  pkgdesc="Header files and scripts for building modules for linux kernel - ${_desc}"
  provides=("linux-headers=${pkgver}")
  conflicts=('linux-headers')

  cd ${_srcname}
  local _builddir="${pkgdir}/usr/lib/modules/${_kernver}/build"

  install -Dt "${_builddir}" -m644 Makefile .config Module.symvers
  install -Dt "${_builddir}/kernel" -m644 kernel/Makefile

  mkdir "${_builddir}/.tmp_versions"

  cp -t "${_builddir}" -a include scripts

  install -Dt "${_builddir}/arch/${KARCH}" -m644 arch/${KARCH}/Makefile
  install -Dt "${_builddir}/arch/${KARCH}/kernel" -m644 arch/${KARCH}/kernel/asm-offsets.s arch/$KARCH/kernel/module.lds

  cp -t "${_builddir}/arch/${KARCH}" -a arch/${KARCH}/include
  mkdir -p "${_builddir}/arch/arm"
  cp -t "${_builddir}/arch/arm" -a arch/arm/include

  install -Dt "${_builddir}/drivers/md" -m644 drivers/md/*.h
  install -Dt "${_builddir}/net/mac80211" -m644 net/mac80211/*.h

  # http://bugs.archlinux.org/task/13146
  install -Dt "${_builddir}/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h

  # http://bugs.archlinux.org/task/20402
  install -Dt "${_builddir}/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
  install -Dt "${_builddir}/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
  install -Dt "${_builddir}/drivers/media/tuners" -m644 drivers/media/tuners/*.h

  # add xfs and shmem for aufs building
  mkdir -p "${_builddir}"/{fs/xfs,mm}

  # copy in Kconfig files
  find . -name Kconfig\* -exec install -Dm644 {} "${_builddir}/{}" \;

  # remove unneeded architectures
  local _arch
  for _arch in "${_builddir}"/arch/*/; do
    [[ ${_arch} == */${KARCH}/ || ${_arch} == */arm/ ]] && continue
    rm -r "${_arch}"
  done

  # remove files already in linux-docs package
  rm -r "${_builddir}/Documentation"

  # remove now broken symlinks
  find -L "${_builddir}" -type l -printf 'Removing %P\n' -delete

  # Fix permissions
  chmod -R u=rwX,go=rX "${_builddir}"

  # strip scripts directory
  local _binary _strip
  while read -rd '' _binary; do
    case "$(file -bi "${_binary}")" in
      *application/x-sharedlib*)  _strip="${STRIP_SHARED}"   ;; # Libraries (.so)
      *application/x-archive*)    _strip="${STRIP_STATIC}"   ;; # Libraries (.a)
      *application/x-executable*) _strip="${STRIP_BINARIES}" ;; # Binaries
      *) continue ;;
    esac
    /usr/bin/strip ${_strip} "${_binary}"
  done < <(find "${_builddir}/scripts" -type f -perm -u+w -print0 2>/dev/null)
}

pkgname=("${pkgbase}" "${pkgbase}-headers")
for _p in ${pkgname[@]}; do
  eval "package_${_p}() {
    _package${_p#${pkgbase}}
  }"
done
