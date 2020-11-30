# AArch64 multi-platform
# Maintainer: Kevin Mihelich <kevin@archlinuxarm.org>

buildarch=8

pkgbase=linux-aarch64
_srcname=linux-5.9
_kernelname=${pkgbase#linux}
_desc="AArch64 multi-platform"
pkgver=5.9.11
pkgrel=1
arch=('aarch64')
url="http://www.kernel.org/"
license=('GPL2')
makedepends=('xmlto' 'docbook-xsl' 'kmod' 'inetutils' 'bc' 'git' 'uboot-tools' 'vboot-utils' 'dtc')
options=('!strip')
source=("http://www.kernel.org/pub/linux/kernel/v5.x/${_srcname}.tar.xz"
        "http://www.kernel.org/pub/linux/kernel/v5.x/patch-${pkgver}.xz"
        '0001-phy-rockchip-add-rockchip-usb3-innosilicon-phy-drive.patch'
        '0002-usb-dwc3-add-rockchip-innosilicon-usb3-glue-layer.patch'
        '0003-arm64-dts-rockchip-add-rk3328-usb3-and-usb3phy-nodes.patch'
        '0004-arm64-dts-rockchip-enable-usb3-on-rk3328-roc-cc-boar.patch'
        '0005-arm64-dts-rockchip-rk3328-roc-cc-Set-dr_mode-to-host.patch'
        '0006-arm64-dts-rockchip-rk3328-roc-cc-Enable-HDMI-audio.patch'
        '0007-arm64-dts-rockchip-rk3328-roc-cc-Enable-analog-audio.patch'
        '0008-board-rk3328-roc-cc-adjust-DMC-opps.patch'
        '0009-arm64-dts-rockchip-add-more-cpu-operating-points-for.patch'
        '0010-arm64-dts-rockchip-Add-RK3328-GPU-OPPs.patch'
        '0011-arm64-dts-rk805-enable-rtc-when-power-off.patch'
        '0012-arm64-dts-rockchip-roc-rk3328-cc-enable-w1-gpio.patch'
        'config'
        'linux.preset'
        '60-linux.hook'
        '90-linux.hook')
md5sums=('0959d759fd19e146367221aff504ad91'
         'f400a38fe1f390748ac9d3a2b130858c'
         'd4d5ef608e6847b33fd1228010b5a9b7'
         '7236bc43b784f7a21eae1dd5e367cf42'
         'dc7700f98355e60db663fa3ddeeeaa52'
         'e7d55054bdd76ab793338bf80d9f8f65'
         '9c87ed830c471858588ffa255553e658'
         '793c1e2111f5df6c329e3966ec2f0a7f'
         '0ec622273e58c1e5f8e0c6f7d819ba17'
         'babf7c814e8fe2d343b96e7a348dd6c4'
         '714299ed13c8734994344f276cf99872'
         '15ccf75b10d59596550d510dbab5d485'
         '18a95778ab7418fa0a7164bc81bec4fa'
         '75f664c9c670b8cfeaac9044ae716771'
         'd483adf9941f8488d8bcd4e39ce227b5'
         '41cb5fef62715ead2dd109dbea8413d6'
         'ce6c81ad1ad1f8b333fd6077d47abdaf'
         '3dc88030a8f2f5a5f97266d99b149f77')

prepare() {
  cd ${_srcname}

  # add upstream patch
  git apply --whitespace=nowarn ../patch-${pkgver}

  # ALARM patches
  git apply ../0001-phy-rockchip-add-rockchip-usb3-innosilicon-phy-drive.patch
  git apply ../0002-usb-dwc3-add-rockchip-innosilicon-usb3-glue-layer.patch
  git apply ../0003-arm64-dts-rockchip-add-rk3328-usb3-and-usb3phy-nodes.patch
  git apply ../0004-arm64-dts-rockchip-enable-usb3-on-rk3328-roc-cc-boar.patch
  git apply ../0005-arm64-dts-rockchip-rk3328-roc-cc-Set-dr_mode-to-host.patch
  git apply ../0006-arm64-dts-rockchip-rk3328-roc-cc-Enable-HDMI-audio.patch
  git apply ../0007-arm64-dts-rockchip-rk3328-roc-cc-Enable-analog-audio.patch
  git apply ../0008-board-rk3328-roc-cc-adjust-DMC-opps.patch
  git apply ../0009-arm64-dts-rockchip-add-more-cpu-operating-points-for.patch
  git apply ../0010-arm64-dts-rockchip-Add-RK3328-GPU-OPPs.patch
  git apply ../0011-arm64-dts-rk805-enable-rtc-when-power-off.patch
  git apply ../0012-arm64-dts-rockchip-roc-rk3328-cc-enable-w1-gpio.patch

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

  yes "" | make config

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
  provides=("linux=${pkgver}" "WIREGUARD-MODULE")
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
