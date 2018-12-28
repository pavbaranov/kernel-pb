# Maintainer: Tom Nguyen <tom81094@gmail.com>
# Maintainer: Piotr Gorski <lucjan.lucjanov@gmail.com>
# Contributor: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>
# Contributor: Tobias Powalowski <tpowa@archlinux.org>
# Contributor: Thomas Baechler <thomas@archlinux.org>

### BUILD OPTIONS
# Set these variables to ANYTHING that is not null to enable them

### Set performance governor as default
_per_gov=y

# NUMA is optimized for multi-socket motherboards. A single multi-core CPU can
# actually run slower with NUMA enabled. Most users will want to set this option
# to enabled ... in other words, do not use NUMA on a single CPU system.
#
# See, https://bugs.archlinux.org/task/31187
_NUMAdisable=y

# Compile ONLY probed modules
# As of mainline 2.6.32, running with this option will only build the modules
# that you currently have probed in your system VASTLY reducing the number of
# modules built and the build time to do it.
#
# WARNING - ALL modules must be probed BEFORE you begin making the pkg!
#
# To keep track of which modules are needed for your specific system/hardware,
# give module_db script a try: https://aur.archlinux.org/packages/modprobed-db
# This PKGBUILD will call it directly to probe all the modules you have logged!
#
# More at this wiki page ---> https://wiki.archlinux.org/index.php/Modprobed-db
_localmodcfg=y

# Use the current kernel's .config file
# Enabling this option will use the .config of the RUNNING kernel rather than
# the ARCH defaults. Useful when the package gets updated and you already went
# through the trouble of customizing your config options.  NOT recommended when
# a new kernel is released, but again, convenient for package bumps.
_use_current=y

### Disable Deadline I/O scheduler
_deadline_disable=y

### Disable CFQ I/O scheduler
_CFQ_disable=y

### Disable Kyber I/O scheduler
_kyber_disable=y

### Disable MQ scheduling
_mq_disable=

### Running with a 1000 HZ tick rate
_1k_HZ_ticks=y

### Do no edit below this line unless you know what you're doing

pkgbase=linux-pb
#pkgbase=linux-custom       # Build kernel with a different name
_major=4.20
pkgver=4.20
_srcpatch="${pkgver}"
_srcname="linux-${pkgver}"
pkgrel=3
arch=('x86_64')
url="https://github.com/Algodev-github/bfq-mq/"
license=('GPL2')
makedepends=('kmod' 'inetutils' 'bc' 'libelf' 'lzop')
options=('!strip')
_bfqpath="https://gitlab.com/tom81094/custom-patches/raw/master/bfq-mq"
_lucjanpath="https://gitlab.com/sirlucjan/kernel-patches/raw/master/4.20"
_lucjanpath_2="https://raw.githubusercontent.com/sirlucjan/kernel-patches/master/4.20"
_gcc_path="https://raw.githubusercontent.com/graysky2/kernel_gcc_patch/master"
_gcc_patch="enable_additional_cpu_optimizations_for_gcc_v8.1+_kernel_v4.13+.patch"
_bfq_sq_mq_path="bfq-sq-mq"
_bfq_sq_mq_ver='v9r1'
_bfq_sq_mq_rel='2K181212-rc1'
_bfq_sq_mq_patch="${_major}-bfq-sq-mq-${_bfq_sq_mq_ver}-${_bfq_sq_mq_rel}.patch"
_uksm_path="https://raw.githubusercontent.com/dolohow/uksm/master"
_uksm_patch_2="https://raw.githubusercontent.com/zaza42/uksm/master"
_uksm_ver="uksm-${_major}"
_uksm_ver_2="uksm-${_major}-rc1"
_pds_path="https://gitlab.com/alfredchen/PDS-mq/raw/master/${_major}"
_pds_ver=v4.20_pds099i
_pavbaranov_path="https://raw.githubusercontent.com/pavbaranov/kernel-pb/master"

source=(# mainline kernel patches
        "https://www.kernel.org/pub/linux/kernel/v4.x/${_srcname}.tar.xz"
        "https://www.kernel.org/pub/linux/kernel/v4.x/${_srcname}.tar.sign"
        # gcc cpu optimizatons from graysky and ck
        "${_gcc_path}/${_gcc_patch}"
        # bfq-mq patch
        "${_lucjanpath}/${_bfq_sq_mq_path}/${_bfq_sq_mq_patch}"
        "${_lucjanpath_2}/${_bfq_sq_mq_path}-dev/0001-bfq-Increase-BLKCG_MAX_POLS.patch"
        # Additional patches
        "${_lucjanpath}/0100-Check-presence-on-tree-of-every-entity-after-every-a.patch"
        "${_lucjanpath}/pf-miscellaneous/0001-add-sysctl-to-disallow-unprivileged-CLONE_NEWUSER-by.patch"
        # UKSM patch
        "${_uksm_path}/${_uksm_ver}".patch
        # PDS patch
        "${_pds_path}/${_pds_ver}".patch
        Fix-missing-mainline-scheduler-API-for-psi.patch::"https://gitlab.com/alfredchen/linux-pds/commit/b065cb11f1c039edcc2bbd10a82fcaf18b20d87d.diff"
         # the main kernel config files
        'config'
         # pacman hook for depmod
        '60-linux.hook'
         # pacman hook for initramfs regeneration
        '90-linux.hook'
         # pacman hook for remove initramfs
        '99-linux.hook'
         # standard config files for mkinitcpio ramdisk
        'linux.preset'
        # Additional patches
        "${_lucjanpath_2}/pf-fixes-sep/0001-memstick-rtsx_usb_ms-Add-missing-pm_runtime_disable-.patch"
        "${_lucjanpath_2}/pf-fixes-sep/0002-misc-rtsx_usb-Use-USB-remote-wakeup-signaling-for-ca.patch"
        "${_lucjanpath_2}/pf-fixes-sep/0003-memstick-Prevent-memstick-host-from-getting-runtime-.patch"
        "${_lucjanpath_2}/pf-fixes-sep/0004-memstick-rtsx_usb_ms-Use-ms_dev-helper.patch"
        "${_lucjanpath_2}/pf-fixes-sep/0005-memstick-rtsx_usb_ms-Support-runtime-power-managemen.patch"
        "${_lucjanpath_2}/pf-fixes-sep/0006-block-bfq-fix-comments-on-__bfq_deactivate_entity.patch"
        #Alexandre Frade patches from xanmod linux
        "${_pavbaranov_path}/set-128_2048-kb-to-read-ahead-for-filesystem.patch"
        "${_pavbaranov_path}/add-500Hz-timer-interrupt-kernel-config-option.patch"
        "${_pavbaranov_path}/decreases-the-amount-of-swapping.patch"
        )

sha256sums=('ad0823183522e743972382df0aa08fb5ae3077f662b125f1e599b0b2aaa12438'
            'SKIP'
            '9f7177679c8d3f8d699ef0566a51349d828436dba04603bc2223f98c60d2d178'
            '8761152216a204b0bbf2bd581abc3f5cdf851cec8b807316528b72a7b552ef12'
            '2cb5ecec3fc61d86da443570eede67ed11e098f4603e2c1a7d50b3267a88df23'
            'eb3cb1a9e487c54346b798b57f5b505f8a85fd1bc839d8f00b2925e6a7d74531'
            'b436a2bdf49903e0e72c74c836cd3f48c1d722c7c6daa75d63244f866105b000'
            '2da4d705fe5be8ac9b5af68c48ddb5b925f2f756cb84c4c66ad05279676503a1'
            'ea3bb3f97297ac6c5d2feefc428873004e18013333478656a0521d53055b8980'
            'd98895434951e8df12faa0a6f15ffc0958eb81ed56cd754846890defebc15ee3'
            '7670e90fbde0fdb519104d73c407b260eb983e63cd5d6b8ba301164f669a7e99'
            'ae2e95db94ef7176207c690224169594d49445e04249d2499e9d2fbc117a0b21'
            'c043f3033bb781e2688794a59f6d1f7ed49ef9b13eb77ff9a425df33a244a636'
            'ed9d35cb7d7bd829ff6253353efa5e2d119820fe4f4310aea536671f5e4caa37'
            'ad6344badc91ad0630caacde83f7f9b97276f80d26a20619a87952be65492c65'
            '15a62fc2f8c03bdcbc1dd2bab05b677e2808ea37dc13dc19a88adc1bbf88fe5c'
            '4b9214c816bbcd5e18e752b958a22b67e7c6aee56d7fda0d8c3a552980a2caae'
            '87ede2b1d2e287eaa8b672fd25ebbfd3a046b2635190b3374115c4ea8196f6c8'
            '9100e5746d021af84eee6c50f4dd58700ce15a4edbc428667d003973b388e4f7'
            '0ec4d1beddf7f3b6631bc7f5af9811d54886ccfd6362e6c6177975f176453026'
            '772932d2fdb0a71fb78c541a1a1400413ab1cfbc8bad72d95ee365a938432b09'
            'afd45945954e3aab0261943b7b31da224335fc538c820088ea78b20b75d8323f'
            'f035ed25b1dcc24d9bdfa613af10818ac6534849090b07f4c881ea63fbaf217f'
            'faa1c173abd2b69df46c772c61dc68879e2c76a34ca5bb4bbd930f599c77b114')
validpgpkeys=(
              '647F28654894E3BD457199BE38DBBDC86092693E' # Greg Kroah-Hartman
             )

_kernelname=${pkgbase#linux}
: ${_kernelname:=-bfq-mq} 

prepare() {
  cd ${_srcname}

  ### Setting version
        msg2 "Setting version..."
        sed -e "/^EXTRAVERSION =/s/=.*/=/" -i Makefile
        scripts/setlocalversion --save-scmversion
        echo "-$pkgrel" > localversion.10-pkgrel
        echo "$_kernelname" > localversion.20-pkgname

    ### Patching sources
        local src
        for src in "${source[@]}"; do
            src="${src%%::*}"
            src="${src##*/}"
            [[ $src = *.patch ]] || continue
        msg2 "Applying patch $src..."
        patch -Np1 < "../$src"
        done

    ### Setting config
        msg2 "Setting config..."
        cp ../config .config
        make olddefconfig

    ### Prepared version
        make -s kernelrelease > ../version
        msg2 "Prepared %s version %s" "$pkgbase" "$(<../version)"

    ### Optionally set tickrate to 1000 
        if [ -n "$_1k_HZ_ticks" ]; then
        msg "Setting tick rate to 1k..."
        sed -i -e 's/^CONFIG_HZ_300=y/# CONFIG_HZ_300 is not set/' \
            -i -e 's/^# CONFIG_HZ_1000 is not set/CONFIG_HZ_1000=y/' \
            -i -e 's/^CONFIG_HZ=300/CONFIG_HZ=1000/' ./.config
        fi

    ### Enable fancontrol
        if [ -n "$_dell_fancontrol" ]; then
        msg "Enabling I8K for Dell..."
        sed -i -e s'/^CONFIG_I8K=m/CONFIG_I8K=y/' \
            -i -e s'/^CONFIG_SENSORS_DELL_SMM=m/CONFIG_SENSORS_DELL_SMM=y/' ./.config    
        fi

    ### Set performance governor
        if [ -n "$_per_gov" ]; then
        msg "Setting performance governor.."
        sed -i -e s'/^CONFIG_CPU_FREQ_DEFAULT_GOV_SCHEDUTIL=y/# CONFIG_CPU_FREQ_DEFAULT_GOV_SCHEDUTIL is not set/' \
            -i -e s'/^# CONFIG_CPU_FREQ_DEFAULT_GOV_PERFORMANCE is not set/CONFIG_CPU_FREQ_DEFAULT_GOV_PERFORMANCE=y/' ./.config
        msg "Disabling uneeded governors..."
        sed -i -e s'/^CONFIG_CPU_FREQ_GOV_ONDEMAND=m/# CONFIG_CPU_FREQ_GOV_ONDEMAND is not set/' \
            -i -e s'/^CONFIG_CPU_FREQ_GOV_CONSERVATIVE=m/# CONFIG_CPU_FREQ_GOV_CONSERVATIVE is not set/' \
            -i -e s'/^CONFIG_CPU_FREQ_GOV_USERSPACE=m/# CONFIG_CPU_FREQ_GOV_USERSPACE is not set/' \
            -i -e s'/^CONFIG_CPU_FREQ_GOV_SCHEDUTIL=y/# CONFIG_CPU_FREQ_GOV_SCHEDUTIL is not set/' ./.config
        fi

  ### Optionally disable NUMA for 64-bit kernels only
        # (x86 kernels do not support NUMA)
        if [ -n "$_NUMAdisable" ]; then
            msg "Disabling NUMA from kernel config..."
            sed -i -e 's/CONFIG_NUMA=y/# CONFIG_NUMA is not set/' \
                -i -e '/CONFIG_AMD_NUMA=y/d' \
                -i -e '/CONFIG_X86_64_ACPI_NUMA=y/d' \
                -i -e '/CONFIG_NODES_SPAN_OTHER_NODES=y/d' \
                -i -e '/# CONFIG_NUMA_EMU is not set/d' \
                -i -e '/CONFIG_NODES_SHIFT=6/d' \
                -i -e '/CONFIG_NEED_MULTIPLE_NODES=y/d' \
                -i -e '/# CONFIG_MOVABLE_NODE is not set/d' \
                -i -e '/CONFIG_USE_PERCPU_NUMA_NODE_ID=y/d' \
                -i -e '/CONFIG_ACPI_NUMA=y/d' ./.config
        fi

    ### Optionally use running kernel's config
        # code originally by nous; http://aur.archlinux.org/packages.php?ID=40191
        if [ -n "$_use_current" ]; then
            if [[ -s /proc/config.gz ]]; then
            msg "Extracting config from /proc/config.gz..."
            # modprobe configs
            zcat /proc/config.gz > ./.config
        else
            warning "Your kernel was not compiled with IKCONFIG_PROC!"
            warning "You cannot read the current config!"
            warning "Aborting!"
            exit
            fi
        fi

    ### Disable Deadline I/O scheduler
        if [ -n "$_deadline_disable" ]; then
        msg "Disabling Deadline I/O scheduler..."
        sed -i -e s'/CONFIG_IOSCHED_DEADLINE=y/# CONFIG_IOSCHED_DEADLINE is not set/' ./.config
        sed -i -e s'/CONFIG_MQ_IOSCHED_DEADLINE=y/# CONFIG_MQ_IOSCHED_DEADLINE is not set/' ./.config
        fi

    ### Disable CFQ I/O scheduler
        if [ -n "$_CFQ_disable" ]; then
        msg "Disabling CFQ I/O scheduler..."
        sed -i -e s'/^CONFIG_IOSCHED_CFQ=y/# CONFIG_IOSCHED_CFQ is not set/' \
        -i -e s'/^CONFIG_CFQ_GROUP_IOSCHED=y/# CONFIG_CFQ_GROUP_IOSCHED is not set/' ./.config	
        fi

    ### Disable Kyber I/O scheduler
        if [ -n "$_kyber_disable" ]; then
        msg "Disabling Kyber I/O scheduler..."
        sed -i -e s'/CONFIG_MQ_IOSCHED_KYBER=y/# CONFIG_MQ_IOSCHED_KYBER is not set/' ./.config
        fi

    ### Disable MQ scheduling
	if [ -n "$_mq_disable" ]; then
		msg2 "Disabling MQ scheduling..."
		sed -i -e s'/^CONFIG_SCSI_MQ_DEFAULT=y/# CONFIG_SCSI_MQ_DEFAULT is not set/' \
		    -i -e s'/^CONFIG_DM_MQ_DEFAULT=y/# CONFIG_DM_MQ_DEFAULT is not set/' ./.config
        fi



    ### Optionally load needed modules for the make localmodconfig
        # See https://aur.archlinux.org/packages/modprobed-db
        if [ -n "$_localmodcfg" ]; then
        msg2 "If you have modprobed-db installed, running it in recall mode now"
            if [ -e /usr/bin/modprobed-db ]; then
            [[ -x /usr/bin/sudo ]] || {
            echo "Cannot call modprobe with sudo. Install sudo and configure it to work with this user."
            exit 1; }
            sudo /usr/bin/modprobed-db recall
            make localmodconfig
            fi
        fi

    # Configure the kernel. Replace the line below with one of your choice.
    #make menuconfig # CLI menu for configuration
    #make nconfig # new CLI menu for configuration
    make xconfig # X-based configuration
    #make oldconfig # using old config from previous kernel version
    # ... or manually edit .config
  
    # save configuration for later reuse
    cat .config > "${startdir}/config.last"
}

build() {
  cd ${_srcname}

  make bzImage modules htmldocs -j5
}

_package() {
  pkgdesc="The ${pkgbase/linux/Linux} kernel and modules with the BFQ-MQ scheduler, PDS and UKSM"
  depends=('coreutils' 'linux-firmware' 'kmod' 'mkinitcpio>=0.7' 'lzop')
  optdepends=('crda: to set the correct wireless channels of your country' 'modprobed-db: Keeps track of EVERY kernel module that has ever been probed - useful for those of us who make localmodconfig')
  provides=("${pkgbase}=${pkgver}" "linux=${pkgver}")
  backup=("etc/mkinitcpio.d/${pkgbase}.preset")
  install=linux.install

  local kernver="$(<version)"
  local modulesdir="$pkgdir/usr/lib/modules/$kernver"

  cd $_srcname

  msg2 "Installing boot image..."
  # systemd expects to find the kernel here to allow hibernation
  # https://github.com/systemd/systemd/commit/edda44605f06a41fb86b7ab8128dcf99161d2344
  install -Dm644 "$(make -s image_name)" "$modulesdir/vmlinuz"
  install -Dm644 "$modulesdir/vmlinuz" "$pkgdir/boot/vmlinuz-$pkgbase"

  msg2 "Installing modules..."
  make INSTALL_MOD_PATH="$pkgdir/usr" modules_install

  # a place for external modules,
  # with version file for building modules and running depmod from hook
  local extramodules="extramodules$_kernelname"
  local extradir="$pkgdir/usr/lib/modules/$extramodules"
  install -Dt "$extradir" -m644 ../version
  ln -sr "$extradir" "$modulesdir/extramodules"

  # remove build and source links
  rm "$modulesdir"/{source,build}

  msg2 "Installing hooks..."

  # sed expression for following substitutions
  local subst="
    s|%PKGBASE%|$pkgbase|g
    s|%KERNVER%|$kernver|g
    s|%EXTRAMODULES%|$extramodules|g
  "

  # hack to allow specifying an initially nonexisting install file
  sed "$subst" "$startdir/$install" > "$startdir/$install.pkg"
  true && install=$install.pkg

  # fill in mkinitcpio preset and pacman hooks
  sed "$subst" ../linux.preset | install -Dm644 /dev/stdin \
    "$pkgdir/etc/mkinitcpio.d/$pkgbase.preset"
  sed "$subst" ../60-linux.hook | install -Dm644 /dev/stdin \
    "$pkgdir/usr/share/libalpm/hooks/60-${pkgbase}.hook"
  sed "$subst" ../90-linux.hook | install -Dm644 /dev/stdin \
    "$pkgdir/usr/share/libalpm/hooks/90-${pkgbase}.hook"
  sed "$subst" ../99-linux.hook | install -Dm644 /dev/stdin \
    "$pkgdir/usr/share/libalpm/hooks/99-${pkgbase}.hook"

  msg2 "Fixing permissions..."
  chmod -Rc u=rwX,go=rX "$pkgdir"
}

_package-headers() {
  pkgdesc="Header files and scripts for building modules for ${pkgbase/linux/Linux} kernel"
  provides=("${pkgbase}-headers=${pkgver}" "linux-headers=${pkgver}")
  depends=("${pkgbase}=${pkgver}")

    local builddir="$pkgdir/usr/lib/modules/$(<version)/build"

  cd $_srcname

  msg2 "Installing build files..."
  install -Dt "$builddir" -m644 Makefile .config Module.symvers System.map vmlinux
  install -Dt "$builddir/kernel" -m644 kernel/Makefile
  install -Dt "$builddir/arch/x86" -m644 arch/x86/Makefile
  cp -t "$builddir" -a scripts

  # add objtool for external module building and enabled VALIDATION_STACK option
  install -Dt "$builddir/tools/objtool" tools/objtool/objtool

  # add xfs and shmem for aufs building
  mkdir -p "$builddir"/{fs/xfs,mm}

  # ???
  mkdir "$builddir/.tmp_versions"

  msg2 "Installing headers..."
  cp -t "$builddir" -a include
  cp -t "$builddir/arch/x86" -a arch/x86/include
  install -Dt "$builddir/arch/x86/kernel" -m644 arch/x86/kernel/asm-offsets.s

  install -Dt "$builddir/drivers/md" -m644 drivers/md/*.h
  install -Dt "$builddir/net/mac80211" -m644 net/mac80211/*.h

  # http://bugs.archlinux.org/task/13146
#  install -Dt "$builddir/drivers/media/i2c" -m644 drivers/media/i2c/msp3400-driver.h

  # http://bugs.archlinux.org/task/20402
#  install -Dt "$builddir/drivers/media/usb/dvb-usb" -m644 drivers/media/usb/dvb-usb/*.h
#  install -Dt "$builddir/drivers/media/dvb-frontends" -m644 drivers/media/dvb-frontends/*.h
 # install -Dt "$builddir/drivers/media/tuners" -m644 drivers/media/tuners/*.h

  msg2 "Installing KConfig files..."
  find . -name 'Kconfig*' -exec install -Dm644 {} "$builddir/{}" \;

  msg2 "Removing unneeded architectures..."
  local arch
  for arch in "$builddir"/arch/*/; do
    [[ $arch = */x86/ ]] && continue
    echo "Removing $(basename "$arch")"
    rm -r "$arch"
  done

  msg2 "Removing documentation..."
  rm -r "$builddir/Documentation"

  msg2 "Removing broken symlinks..."
  find -L "$builddir" -type l -printf 'Removing %P\n' -delete

  msg2 "Removing loose objects..."
  find "$builddir" -type f -name '*.o' -printf 'Removing %P\n' -delete

  msg2 "Stripping build tools..."
  local file
  while read -rd '' file; do
    case "$(file -bi "$file")" in
      application/x-sharedlib\;*)      # Libraries (.so)
        strip -v $STRIP_SHARED "$file" ;;
      application/x-archive\;*)        # Libraries (.a)
        strip -v $STRIP_STATIC "$file" ;;
      application/x-executable\;*)     # Binaries
        strip -v $STRIP_BINARIES "$file" ;;
      application/x-pie-executable\;*) # Relocatable binaries
        strip -v $STRIP_SHARED "$file" ;;
    esac
  done < <(find "$builddir" -type f -perm -u+x ! -name vmlinux -print0)

  msg2 "Adding symlink..."
  mkdir -p "$pkgdir/usr/src"
  ln -sr "$builddir" "$pkgdir/usr/src/$pkgbase-$pkgver"
  
  msg2 "Fixing permissions..."
  chmod -Rc u=rwX,go=rX "$pkgdir"
}

pkgname=("$pkgbase" "$pkgbase-headers")
for _p in "${pkgname[@]}"; do
  eval "package_$_p() {
    $(declare -f "_package${_p#$pkgbase}")
    _package${_p#$pkgbase}
  }"
done

# vim:set ts=8 sts=2 sw=2 et:
