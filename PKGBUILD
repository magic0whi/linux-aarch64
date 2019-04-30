# AArch64 multi-platform
# Maintainer: Kevin Mihelich <kevin@archlinuxarm.org>

buildarch=8

pkgbase=linux-aarch64
_srcname=linux-5.0
_kernelname=${pkgbase#linux}
_desc="AArch64 multi-platform"
pkgver=5.0.10
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
        '0005-arm64-dts-rockchip-move-rk3328-sound-dai-cells-to-th.patch'
        '0006-arm64-dts-rockchip-enable-analog-audio-node-for-rock.patch'
        '0007-staging-video-rockchip-add-v4l2-decoder.patch'
        '0008-rockchip-mpp-rkvdec-rbsp.patch'
        '0009-rockchip-mpp-HEVC-decoder-ctrl-data.patch'
        '0010-rockchip-mpp-H.264-decoder-ctrl-data.patch'
        '0011-rockchip-mpp-support-qtable.patch'
        '0012-rockchip-mpp-vdpu2-move-qtable-to-input-buffer.patch'
        '0013-rkvdec-spspps-address-alignment.patch'
        '0014-arm64-dts-rockchip-boost-clocks-for-rk3328.patch'
        '0015-arm64-dts-rockchip-add-video-codec-for-rk3328.patch'
        '0016-arm64-dts-rockchip-enable-HDMI-CEC-on-rk3328.patch'
        '0017-arm64-dts-rockchip-fix-rk3328-roc-cc-gmac2io-stabili.patch'
        '0018-arm64-dts-rockchip-fix-rk3328-roc-cc-gmac2io-tx-rx_d.patch'
        '0019-arm64-dts-rockchip-set-TX-PBL-for-rk3328-roc-cc-gmac.patch'
        '0020-arm64-dts-rockchip-enable-display-nodes-on-rk3328-ro.patch'
        '0021-arm64-dts-rockchip-enable-video-decoder-nodes-on-roc.patch'
        '0022-arm64-dts-rockchip-enable-usb3-nodes-on-roc-rk3328-c.patch'
        '0023-arm64-dts-rockchip-make-USB2.0-port-works-on-host-mo.patch'
        '0024-arm64-dts-rockchip-give-some-life-to-the-rk3328-roc-.patch'
        '0025-arm64-dts-rockchip-add-more-cpu-operating-points-for.patch'
        '0026-arm64-dts-rockchip-add-rk3328-roc-cc-cpu-supply-entr.patch'
        '0027-arm64-dts-Remove-inconsistent-use-of-arm-armv8-compa.patch'
        '0028-clk-rockchip-fix-wrong-clock-definitions-for-rk3328.patch'
        '0029-arm64-dts-rockchip-eMMC-additions-for-rk3328-roc-cc.patch'
        'config'
        'linux.preset'
        '60-linux.hook'
        '90-linux.hook')
md5sums=('7381ce8aac80a01448e065ce795c19c0'
         'a46bbfe17039c1fa81edc847af5ea664'
         '2aadfdfe48b141dccca5f4d6bad5391c'
         'eb3166ea6b4bcf187cabfb518aed44ce'
         '07d1b2299a0995babc45d42a0a96a7b3'
         'd190cf3ddc7b12a9548a95ed02ba1598'
         '306a1bf73ffcf5d96d8999a4e39e65e9'
         '7700d55025641f401718bf7217266ca7'
         '5b48e4fc80f5ebe69e3907f5b476d344'
         'f115824dcb19a7879c054446c53aa21b'
         '3cfd9ed9e5d354ea96ed416707aa45c1'
         '8fae1fc6d462e17900776042ef20b884'
         'ed2ebe9b7c4b263c7ee2e713b5b97083'
         'b167bb37db4f52b330e9dabe0e54cd0e'
         'fdfa64bd2a23cf5aee631fc13ee3560a'
         '6b05cebe4e79924f0c317cf58d44f984'
         '54128b49b0c6c41cfa1f26b0fad977e2'
         'c4def79aae10a5354bebf7d5fc9f39e4'
         'fa0c60419f5b955a5e69e4a5f977e7bf'
         'e0dcebab661a3b61cbc282627d0ae20c'
         '15d27970133e34fc2b0e068f501f3bcb'
         'f6bc7151ae9b5e11092ac0c966376457'
         'eaf6bf0e0df72f76cdcc8e0b1639f6a4'
         '943793515232c1465d64a1d3f9654b09'
         'd971da59bedee94b194f2d3781c8675b'
         'a67541cb1079968a015a797806337635'
         '67a1009a5656202622bd990aec80afb7'
         '3c786974eda167eda19751990f52160d'
         'c36767a59499fb96dd14f974714090f4'
         '705883b16f7225dfa875968da8da992c'
         'dac24bfe69e0f2de1e65103fd2115551'
         '2e53e827641d0254dcf179b117772ba4'
         '41cb5fef62715ead2dd109dbea8413d6'
         'ce6c81ad1ad1f8b333fd6077d47abdaf'
         '3dc88030a8f2f5a5f97266d99b149f77')

prepare() {
  cd "${srcdir}/${_srcname}"

  # add upstream patch
  git apply --whitespace=nowarn ../patch-${pkgver}

  # ALARM patches
  git apply ../0001-net-smsc95xx-Allow-mac-address-to-be-set-as-a-parame.patch
  git apply ../0002-arm64-dts-rockchip-disable-pwm0-on-rk3399-firefly.patch
  git apply ../0003-arm64-dts-rockchip-add-usb3-controller-node-for-RK33.patch
  git apply ../0004-arm64-dts-rockchip-enable-usb3-nodes-on-rk3328-rock6.patch
  git apply ../0005-arm64-dts-rockchip-move-rk3328-sound-dai-cells-to-th.patch
  git apply ../0006-arm64-dts-rockchip-enable-analog-audio-node-for-rock.patch
  git apply ../0007-staging-video-rockchip-add-v4l2-decoder.patch
  git apply ../0008-rockchip-mpp-rkvdec-rbsp.patch
  git apply ../0009-rockchip-mpp-HEVC-decoder-ctrl-data.patch
  git apply ../0010-rockchip-mpp-H.264-decoder-ctrl-data.patch
  git apply ../0011-rockchip-mpp-support-qtable.patch
  git apply ../0012-rockchip-mpp-vdpu2-move-qtable-to-input-buffer.patch
  git apply ../0013-rkvdec-spspps-address-alignment.patch
  git apply ../0014-arm64-dts-rockchip-boost-clocks-for-rk3328.patch
  git apply ../0015-arm64-dts-rockchip-add-video-codec-for-rk3328.patch
  git apply ../0016-arm64-dts-rockchip-enable-HDMI-CEC-on-rk3328.patch
  git apply ../0017-arm64-dts-rockchip-fix-rk3328-roc-cc-gmac2io-stabili.patch
  git apply ../0018-arm64-dts-rockchip-fix-rk3328-roc-cc-gmac2io-tx-rx_d.patch
  git apply ../0019-arm64-dts-rockchip-set-TX-PBL-for-rk3328-roc-cc-gmac.patch
  git apply ../0020-arm64-dts-rockchip-enable-display-nodes-on-rk3328-ro.patch
  git apply ../0021-arm64-dts-rockchip-enable-video-decoder-nodes-on-roc.patch
  git apply ../0022-arm64-dts-rockchip-enable-usb3-nodes-on-roc-rk3328-c.patch
  git apply ../0023-arm64-dts-rockchip-make-USB2.0-port-works-on-host-mo.patch
  git apply ../0024-arm64-dts-rockchip-give-some-life-to-the-rk3328-roc-.patch
  git apply ../0025-arm64-dts-rockchip-add-more-cpu-operating-points-for.patch
  git apply ../0026-arm64-dts-rockchip-add-rk3328-roc-cc-cpu-supply-entr.patch
  git apply ../0027-arm64-dts-Remove-inconsistent-use-of-arm-armv8-compa.patch
  git apply ../0028-clk-rockchip-fix-wrong-clock-definitions-for-rk3328.patch
  git apply ../0029-arm64-dts-rockchip-eMMC-additions-for-rk3328-roc-cc.patch

  cat "${srcdir}/config" > ./.config

  # add pkgrel to extraversion
  sed -ri "s|^(EXTRAVERSION =)(.*)|\1 \2-${pkgrel}|" Makefile

  # don't run depmod on 'make install'. We'll do this ourselves in packaging
  sed -i '2iexit 0' scripts/depmod.sh
}

build() {
  cd "${srcdir}/${_srcname}"

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

  cd "${srcdir}/${_srcname}"

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

  install -dm755 "${pkgdir}/usr/lib/modules/${_kernver}"

  cd "${srcdir}/${_srcname}"
  install -D -m644 Makefile \
    "${pkgdir}/usr/lib/modules/${_kernver}/build/Makefile"
  install -D -m644 kernel/Makefile \
    "${pkgdir}/usr/lib/modules/${_kernver}/build/kernel/Makefile"
  install -D -m644 .config \
    "${pkgdir}/usr/lib/modules/${_kernver}/build/.config"

  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/include"

  for i in acpi asm-generic clocksource config crypto drm generated keys linux \
    math-emu media net pcmcia scsi soc sound trace uapi video xen; do
    cp -a include/${i} "${pkgdir}/usr/lib/modules/${_kernver}/build/include/"
  done

  # copy arch includes for external modules
  mkdir -p ${pkgdir}/usr/lib/modules/${_kernver}/build/arch/$KARCH
  cp -a arch/$KARCH/include ${pkgdir}/usr/lib/modules/${_kernver}/build/arch/$KARCH/

  # copy files necessary for later builds, like nvidia and vmware
  cp Module.symvers "${pkgdir}/usr/lib/modules/${_kernver}/build"
  cp -a scripts "${pkgdir}/usr/lib/modules/${_kernver}/build"

  # fix permissions on scripts dir
  chmod og-w -R "${pkgdir}/usr/lib/modules/${_kernver}/build/scripts"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/.tmp_versions"

  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/${KARCH}/kernel"

  cp arch/${KARCH}/Makefile "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/${KARCH}/"

  cp arch/${KARCH}/kernel/asm-offsets.s "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/${KARCH}/kernel/"

  # copy module linker script
  cp arch/$KARCH/kernel/module.lds "${pkgdir}/usr/lib/modules/${_kernver}/build/arch/${KARCH}/kernel/"

  # add dm headers
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/md"
  cp drivers/md/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/md"

  # add inotify.h
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/include/linux"
  cp include/linux/inotify.h "${pkgdir}/usr/lib/modules/${_kernver}/build/include/linux/"

  # add wireless headers
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/net/mac80211/"
  cp net/mac80211/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/net/mac80211/"

  # add dvb headers for external modules
  # in reference to:
  # http://bugs.archlinux.org/task/11194
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/include/config/dvb/"
  cp include/config/dvb/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/include/config/dvb/"

  # add dvb headers for http://mcentral.de/hg/~mrec/em28xx-new
  # in reference to:
  # http://bugs.archlinux.org/task/13146
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-frontends/"
  cp drivers/media/dvb-frontends/lgdt330x.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-frontends/"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/i2c/"
  cp drivers/media/i2c/msp3400-driver.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/i2c/"

  # add dvb headers
  # in reference to:
  # http://bugs.archlinux.org/task/20402
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/usb/dvb-usb"
  cp drivers/media/usb/dvb-usb/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/usb/dvb-usb/"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-frontends"
  cp drivers/media/dvb-frontends/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/dvb-frontends/"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/tuners"
  cp drivers/media/tuners/*.h "${pkgdir}/usr/lib/modules/${_kernver}/build/drivers/media/tuners/"

  # add xfs and shmem for aufs building
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/fs/xfs"
  mkdir -p "${pkgdir}/usr/lib/modules/${_kernver}/build/mm"

  # copy in Kconfig files
  for i in $(find . -name "Kconfig*"); do
    mkdir -p "${pkgdir}"/usr/lib/modules/${_kernver}/build/`echo ${i} | sed 's|/Kconfig.*||'`
    cp ${i} "${pkgdir}/usr/lib/modules/${_kernver}/build/${i}"
  done

  chown -R root.root "${pkgdir}/usr/lib/modules/${_kernver}/build"
  find "${pkgdir}/usr/lib/modules/${_kernver}/build" -type d -exec chmod 755 {} \;

  # strip scripts directory
  find "${pkgdir}/usr/lib/modules/${_kernver}/build/scripts" -type f -perm -u+w 2>/dev/null | while read binary ; do
    case "$(file -bi "${binary}")" in
      *application/x-sharedlib*) # Libraries (.so)
        /usr/bin/strip ${STRIP_SHARED} "${binary}";;
      *application/x-archive*) # Libraries (.a)
        /usr/bin/strip ${STRIP_STATIC} "${binary}";;
      *application/x-executable*) # Binaries
        /usr/bin/strip ${STRIP_BINARIES} "${binary}";;
    esac
  done

  # remove unneeded architectures
  rm -rf "${pkgdir}"/usr/lib/modules/${_kernver}/build/arch/{alpha,arc,arm,arm26,avr32,blackfin,c6x,cris,frv,h8300,hexagon,ia64,m32r,m68k,m68knommu,metag,mips,microblaze,mn10300,openrisc,parisc,powerpc,ppc,s390,score,sh,sh64,sparc,sparc64,tile,unicore32,um,v850,x86,xtensa}
}

pkgname=("${pkgbase}" "${pkgbase}-headers")
for _p in ${pkgname[@]}; do
  eval "package_${_p}() {
    _package${_p#${pkgbase}}
  }"
done
