# Maintainer: nycko123 <nycko123 at gmail>
# Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

### BUILD OPTIONS {{{
# Set these variables to ANYTHING that is not null to enable them

### Tweak kernel options prior to a build via nconfig
_makenconfig=

### Tweak kernel options prior to a build via menuconfig
_makemenuconfig=

### Tweak kernel options prior to a build via xconfig
_makexconfig=y

### Tweak kernel options prior to a build via gconfig
_makegconfig=

### Setting GCC Flags for CONFIG_MHASWELL
_gcc_ivybridge=y

### Enable fancontrol for DELL
#_dell_fancontrol=

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
_deadline_disable=

### Disable CFQ I/O scheduler
_CFQ_disable=y

### Disable Kyber I/O scheduler
_kyber_disable=y

### Enable MQ scheduling
_mq_enable=

### Running with a 1000 HZ tick rate
_1k_HZ_ticks=y

### Enable WireGuard
_net_udp_tunnel=
#}}}

### Do no edit below this line unless you know what you're doing

pkgbase=linux-pb
_major=5.10
_minor=13
pkgver=${_major}.${_minor}
#pkgver=${_major}
_srcname=linux-${pkgver}
pkgrel=1
pkgdesc="linux-pb ${pkgver} = arch1 patches + BMQ ${_major} + UKSM and others"
#S_srctag=v${pkgver%.*}-arch${pkgver##*.}
#url="https://git.archlinux.org/linux.git/log/?h=$_srctag"
url="https://gitlab.com/nycko123/kernel"
arch=(x86_64)
license=(GPL2)
makedepends=(bc kmod libelf pahole xmlto python-sphinx_rtd_theme graphviz imagemagick git)
options=('!strip')
#_srcname=archlinux-linux
#_srcname="linux-${pkgver}"  # stable
_mainname="linux-${_major}"
#_srcname="linux-${pkgver}-rc4"  # mainline
_kernelname="-pb"

### SOURCES URLs {{{
### Arch Linux
_arch_patches="https://git.archlinux.org/linux.git/patch/"

### Clear Linux
_cl_path="https://github.com/clearlinux-pkgs/linux/raw/master"

### gitlab/sirlucjan
_lucjan_path="https://raw.githubusercontent.com/sirlucjan/kernel-patches/master/$_major"

### graysky's gcc
#_gcc_path="https://raw.githubusercontent.com/graysky2/kernel_gcc_patch/master"
#_gcc_patch="enable_additional_cpu_optimizations_for_gcc_v8.1+_kernel_v4.13+.patch"

### Paolo Valente's bfq-dev
#_paolo_path="https://github.com/Algodev-github/bfq-mq/commit"

### github/pavbaranov
#_pavbaranov_path="https://raw.githubusercontent.com/pavbaranov/kernel-pb/master"

### Alfred Chen BMQ
_chen_path="https://gitlab.com/alfredchen/linux-prjc/uploads"
_chen_ver="prjc_v$_major-r2"

## Łukasz Żarnowiecki UKSM
#_uksm_path='https://raw.githubusercontent.com/dolohow/uksm/master'
#_uksm_ver="v5.x/uksm-${_major}.patch"
#}}}

## ZEN _srctag
#_srctag=v${pkgver}.zen1

### source array {{{
source=(
  ## Arch kernel
  #"$_srcname::git+https://git.archlinux.org/linux.git?signed#tag=$_srctag"

  ## stable kernel sources
#  "https://git.archlinux.org/linux.git/snapshot/linux-5.8-arch1.tar.gz"
  "https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-${pkgver}.tar.xz"
  "https://cdn.kernel.org/pub/linux/kernel/v5.x/linux-${pkgver}.tar.sign"
#  "$_srcname::git+https://github.com/zen-kernel/zen-kernel?signed#tag=$_srctag"
  config
#  sphinx-workaround.patch
  ## stable kernel patches
#  "https://cdn.kernel.org/pub/linux/kernel/v5.x/patch-5.5.6.xz"
#  "https://cdn.kernel.org/pub/linux/kernel/v5.x/patch-${pkgver}.xz"
#  "https://cdn.kernel.org/pub/linux/kernel/v5.x/patch-${pkgver}.xz.sign"

  #mainline kernel sources
  #"https://git.kernel.org/torvalds/t/${_srcname}.tar.gz"

  ## Arch patches {{{
"$_lucjan_path/arch-patches-v14/0001-arch-patches.patch"
#}}}

# Block-patches
"$_lucjan_path/block-patches-v3/0001-block-patches.patch"

# clearlinux patches
"$_lucjan_path/clearlinux-patches/0001-clearlinux-patches.patch"

# CPU patches (i.e. Graysky patch)
"$_lucjan_path/cpu-patches-v2/0001-cpu-patches.patch"

# Misc fixes patches
"$_lucjan_path/fixes-miscellaneous-v9/0001-fixes-miscellaneous.patch"

# Futex patches
#"$_lucjan_path/futex-patches-v2/0001-futex-patches.patch"

# IOMAP
#"$_lucjan_path/iomap-patches/0001-iomap-patches.patch"

# KSM
#"$_lucjan_path/ksm-patches/0001-ksm-patches.patch"

# LQX patches
"$_lucjan_path/lqx-patches-v2/0001-lqx-patches.patch"

# UKSM
"$_lucjan_path/uksm-patches/0001-UKSM-for-5.10.patch"

# xanmod
"$_lucjan_path/xanmod-patches/0001-sched-autogroup-Add-kernel-parameter-and-config-opti.patch"

# ZEN 
"$_lucjan_path/zen-patches/0001-zen-patches.patch"

# ZSTD
"$_lucjan_path/zstd-dev-patches/0001-zstd-dev-patches.patch"

 ## prjc patch
"https://gitlab.com/alfredchen/linux-prjc/uploads/cda220f104bd6e07ea6fefa86c709dbe/prjc_v5.10-r2.patch"
#"https://gitlab.com/alfredchen/linux-prjc/uploads/59e187026a3068afe7eafd33883ec7be/prjc_v5.9-r3.patch"

#"$_lucjan_path/prjc-patches-v3/0001-prjc-patches.patch"
#"$_lucjan_path/prjc-lucjan-patches/0001-prjc-lucjan-patches.patch"
#"$_lucjan_path/prjc-trunk-patches-v2/0001-sched-pds-1.1-Implement-bitmap-allocator.patch"

#glitched patches
 #   "https://raw.githubusercontent.com/Frogging-Family/linux-tkg/master/linux58-tkg/linux58-tkg-patches/0003-glitched-base.patch"
 #   "https://raw.githubusercontent.com/Frogging-Family/linux-tkg/master/linux58-tkg/linux58-tkg-patches/0006-add-acs-overrides_iommu.patch"
 #   "https://raw.githubusercontent.com/Frogging-Family/linux-tkg/master/linux58-tkg/linux58-tkg-patches/0003-glitched-cfs.patch"

 # MM patches
 "$_lucjan_path/mm-patches-v4/0001-mm-patches.patch"

    ##

  'config'        # the main kernel config file
  'linux.preset'  # mkinitcpio ramdisk config file

)
#}}}

export KBUILD_BUILD_HOST=archlinux
export KBUILD_BUILD_USER=$pkgbase
export KBUILD_BUILD_TIMESTAMP="$(date -Ru${SOURCE_DATE_EPOCH:+d @$SOURCE_DATE_EPOCH})"

### prepare() {{{
prepare() {
  cd $_srcname

### Setting version
  msg2 "Setting version..."
  scripts/setlocalversion --save-scmversion
  echo "-$pkgrel" > localversion.10-pkgrel
  echo "${_kernelname}" > localversion.20-pkgname

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
  make -s kernelrelease > version
  msg2 "Prepared %s version %s" "$pkgbase" "$(<version)"

### Set GCC flags
  if [ -n "$_gcc_ivybridge"  ]; then
    msg2 "Setting GCC flags for Intel IvyBridge CPU..."
    sed -i -e s'/^CONFIG_GENERIC_CPU=y/# CONFIG_GENERIC_CPU is not set/' \
    -i -e s'/^# CONFIG_MIVYBRIDGE is not set/CONFIG_MIVYBRIDGE=y/' ./.config
  fi

### Optionally set tickrate to 1000
  if [ -n "$_1k_HZ_ticks"  ]; then
    msg "Setting tick rate to 1k..."
    sed -i -e 's/^CONFIG_HZ_300=y/# CONFIG_HZ_300 is not set/' \
    -i -e 's/^# CONFIG_HZ_1000 is not set/CONFIG_HZ_1000=y/' \
    -i -e 's/^CONFIG_HZ=300/CONFIG_HZ=1000/' ./.config
  fi

### Optionally enable DELL fancontrol
#  if [ -n "$_dell_fancontrol"  ]; then
#    msg "Enabling I8K for Dell..."
#    sed -i -e s'/^CONFIG_I8K=m/CONFIG_I8K=y/' \
#    -i -e s'/^CONFIG_SENSORS_DELL_SMM=m/CONFIG_SENSORS_DELL_SMM=y/' ./.config
#  fi

### Optionally set performance governor
  if [ -n "$_per_gov"  ]; then
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
  if [ -n "$_NUMAdisable"  ]; then
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
  if [ -n "$_use_current"  ]; then
    if [[ -s /proc/config.gz  ]]; then
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
  if [ -n "$_deadline_disable"  ]; then
    msg "Disabling Deadline I/O scheduler..."
    sed -i -e s'/CONFIG_IOSCHED_DEADLINE=y/# CONFIG_IOSCHED_DEADLINE is not set/' ./.config
    sed -i -e s'/CONFIG_MQ_IOSCHED_DEADLINE=y/# CONFIG_MQ_IOSCHED_DEADLINE is not set/' ./.config
  fi

### Disable CFQ I/O scheduler
  if [ -n "$_CFQ_disable"  ]; then
    msg "Disabling CFQ I/O scheduler..."
    sed -i -e s'/^CONFIG_IOSCHED_CFQ=y/# CONFIG_IOSCHED_CFQ is not set/' \
    -i -e s'/^CONFIG_CFQ_GROUP_IOSCHED=y/# CONFIG_CFQ_GROUP_IOSCHED is not set/' ./.config
  fi

### Disable Kyber I/O scheduler
  if [ -n "$_kyber_disable"  ]; then
    msg "Disabling Kyber I/O scheduler..."
    sed -i -e s'/CONFIG_MQ_IOSCHED_KYBER=y/# CONFIG_MQ_IOSCHED_KYBER is not set/' ./.config
  fi

### Enable MQ scheduling
  if [ -n "$_mq_enable"  ]; then
    msg "Enable MQ scheduling..."
    sed -i -e s'/^# CONFIG_SCSI_MQ_DEFAULT is not set/CONFIG_SCSI_MQ_DEFAULT=y/' \
    -i -e s'/^# CONFIG_DM_MQ_DEFAULT is not set/CONFIG_DM_MQ_DEFAULT=y/' ./.config
  fi

### Optionally load needed modules for the make localmodconfig
# See https://aur.archlinux.org/packages/modprobed-db
  if [ -n "$_localmodcfg"  ]; then
    msg "If you have modprobed-db installed, running it in recall mode now"
    if [ -e /usr/bin/modprobed-db  ]; then
      [[ -x /usr/bin/sudo  ]] || {
      echo "Cannot call modprobe with sudo. Install sudo and configure it to work with this user."
      exit 1; }
      sudo /usr/bin/modprobed-db recall
    fi
    msg "Running Steven Rostedt's make localmodconfig now"
    make localmodconfig
  fi

### Enable WireGuard
  if [ -n "$_net_udp_tunnel"  ]; then
    msg2 "Enabling WireGuard..."
    sed -i -e 's/^CONFIG_NET_UDP_TUNNEL=m/CONFIG_NET_UDP_TUNNEL=y/' ./.config
  fi

### Running make nconfig
  [[ -z "$_makenconfig"  ]] ||  make nconfig
### Running make menuconfig
  [[ -z "$_makemenuconfig"  ]] || make menuconfig
### Running make xconfig
  [[ -z "$_makexconfig"  ]] || make xconfig
### Running make gconfig
  [[ -z "$_makegconfig"  ]] || make gconfig

### save configuration for later reuse
  cat .config > "${startdir}/config.last"
}
#}}}

### build() {{{
build() {
  cd $_srcname
  #make bzImage modules htmldocs
  make bzImage modules
}
#}}}

### _package() {{{
_package() {
  pkgdesc="The $pkgdesc kernel and modules with GCC, BFQ-dev, BMQ, UKSM and other patches"
  depends=(coreutils kmod mkinitcpio initramfs)
  optdepends=('crda: to set the correct wireless channels of your country'
              'modprobed-db: Keeps track of EVERY kernel module that has ever been probed - useful for those of us who make localmodconfig'
              'linux-firmware: firmware images needed for some devices')
  provides=("${pkgbase}=${pkgver}" "linux=${pkgver}")
  backup=("etc/mkinitcpio.d/${pkgbase}.preset")
  
  cd $_srcname
  local kernver="$(<version)"
  local modulesdir="$pkgdir/usr/lib/modules/$kernver"

  msg2 "Installing boot image..."
  # systemd expects to find the kernel here to allow hibernation
  # https://github.com/systemd/systemd/commit/edda44605f06a41fb86b7ab8128dcf99161d2344
  install -Dm644 "$(make -s image_name)" "$modulesdir/vmlinuz"

  # Used by mkinitcpio to name the kernel
  echo "$pkgbase" | install -Dm644 /dev/stdin "$modulesdir/pkgbase"

  msg2 "Installing modules..."
  make INSTALL_MOD_PATH="$pkgdir/usr" modules_install

  # remove build and source links
  rm "$modulesdir"/{source,build}

  # installing preset
  msg2 "Installing preset..."
  # sed expression for following substitutions
  local subst="s|%PKGBASE%|$pkgbase|g"
  # fill in mkinitcpio preset
  sed "$subst" ../linux.preset | install -Dm644 /dev/stdin "$pkgdir/etc/mkinitcpio.d/$pkgbase.preset"

  msg2 "Fixing permissions..."
  chmod -Rc u=rwX,go=rX "$pkgdir"
}
#}}}

### _package-headers() {{{
_package-headers() {
  pkgdesc="Headers and scripts for building modules for the $pkgdesc kernel"
  provides=("${pkgbase}-headers=${pkgver}" "linux-headers=${pkgver}")
  depends=("${pkgbase}=${pkgver}")

  cd $_srcname
  local builddir="$pkgdir/usr/lib/modules/$(<version)/build"

  msg2 "Installing build files..."
  install -Dt "$builddir" -m644 .config Makefile Module.symvers System.map \
    localversion.* version vmlinux
  install -Dt "$builddir/kernel" -m644 kernel/Makefile
  install -Dt "$builddir/arch/x86" -m644 arch/x86/Makefile
  cp -t "$builddir" -a scripts

  # add objtool for external module building and enabled VALIDATION_STACK option
  install -Dt "$builddir/tools/objtool" tools/objtool/objtool

  # add xfs and shmem for aufs building
#  mkdir -p "$builddir"/{fs/xfs,mm}

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
#  install -Dt "$builddir/drivers/media/tuners" -m644 drivers/media/tuners/*.h

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
  ln -sr "$builddir" "$pkgdir/usr/src/$pkgbase"

  msg2 "Fixing permissions..."
  chmod -Rc u=rwX,go=rX "$pkgdir"
}
#}}}

### _package-docs() {{{
#_package-docs() {
#  pkgdesc="Kernel hackers manual - HTML documentation that comes with the ${pkgbase/linux/Linux} kernel"
#  provides=("${pkgbase}-docs=${pkgver}" "linux-docs=${pkgver}")
#  depends=("${pkgbase}=${pkgver}")

#  cd $_srcname
#  local builddir="$pkgdir/usr/lib/modules/$(<version)/build"

#  msg2 "Installing documentation..."
#  mkdir -p "$builddir"
#  cp -t "$builddir" -a Documentation

#  msg2 "Removing unneeded files..."
#  rm -rv "$builddir"/Documentation/{,output/}.[^.]*

#  msg2 "Moving HTML docs..."
#  local src dst
#  while read -rd '' src; do
#    dst="$builddir/Documentation/${src#$builddir/Documentation/output/}"
#    mkdir -p "${dst%/*}"
#    mv "$src" "$dst"
#    rmdir -p --ignore-fail-on-non-empty "${src%/*}"
#  done < <(find "$builddir/Documentation/output" -type f -print0)

#  msg2 "Adding symlink..."
#  mkdir -p "$pkgdir/usr/share/doc"
#  ln -sr "$builddir/Documentation" "$pkgdir/usr/share/doc/$pkgbase"

#  msg2 "Fixing permissions..."
#  chmod -Rc u=rwX,go=rX "$pkgdir"
#}
#}}}

#pkgname=("$pkgbase" "$pkgbase-headers" "$pkgbase-docs")
pkgname=("$pkgbase" "$pkgbase-headers")
for _p in "${pkgname[@]}"; do
  eval "package_$_p() {
    $(declare -f "_package${_p#$pkgbase}")
    _package${_p#$pkgbase}
  }"
done

### sha256sums {{{
sha256sums=('06698c0ce35ceefa9b79ceb108ec7fb86de05f51fe615f3ae5cc82e293dfe1f2'
            'SKIP'
            '36439a90c9d2f860298d90e141f3bf9d897dd8ece9e21cd46508f4ed7b2151bb'
            '9ec9ac50a8bdd645c456feab4a0ca9b7ffe6dcd0933a89ba96112f8bdedbf0ae'
            'a580f8437dff7b385bef9e85f33913c8912649b1a000ab8ad755c834338b190e'
            '1389c0e4ca9b0bdc4d7dea84cb1ddb281c75b7aaadcfb22456a612784a41ea85'
            '152e251586eec29990fa4cc30c561b7e49acb765434b70634501b398e4c1fe2e'
            '3caa397a61f00170697d97063e62bd3a33461b78f457cd3b8afc73f2a826f46d'
            '18fe026fb86347956175354ee6df613f4143859435b5689690f5a0e43e06f1a9'
            '9f7931fe587cfbc918aabbf3a1211a7179c8b2b300a1fc38c22920df4ed7dc2a'
            '0b636a0d9577c8c98f54e78c96b675345388d3ab430691fb3b110b9dd55df1ca'
            'cc510600a1d0a9a47337973247aefb824434a9477436975330165167445653a6'
            '1c4701919e9d0c9eec35d325fd4841dfae6377a4f985311cb66c53d4f2e68db0'
            'e308292fc42840a2366280ea7cf26314e92b931bb11f04ad4830276fc0326ee1'
            '710649bd760cbb8529951c4588494e8e56cd22620b8aee5fe04f67b895a470cd'
            '36439a90c9d2f860298d90e141f3bf9d897dd8ece9e21cd46508f4ed7b2151bb'
            '4265eeeb540e63ecd1570cdfd0afaf751e01f65627149eb0f2ce75129991f566')
#}}}

validpgpkeys=(
  'ABAF11C65A2970B130ABE3C479BE3E4300411886'  # Linus Torvalds
  '647F28654894E3BD457199BE38DBBDC86092693E'  # Greg Kroah-Hartman
  '8218F88849AAC522E94CF470A5E9288C4FA415FA'  # Jan Alexander Steffens (heftig)
)
# vim:set ts=8 sts=2 sw=2 et foldenable foldmethod=marker:
