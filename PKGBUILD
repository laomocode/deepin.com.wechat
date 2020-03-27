# Maintainer: Codist <countstarlight@gmail.com>
# Maintainer: laomocode <3344907598@qq.com>
pkgname=deepin.com.wechat
pkgver=2.6.8.65
_deepinwechatver=2.6.8.65deepin0
pkgrel=2
pkgdesc="Tencent WeChat (com.wechat) on Deepin Wine For Archlinux"
arch=("x86_64")
url="https://weixin.qq.com/"
license=('custom')
depends=('p7zip' 'deepin-wine' 'xorg-xwininfo' 'wqy-microhei' 'lib32-alsa-lib' 'lib32-alsa-plugins' 'lib32-libpulse' 'lib32-openal' 'lib32-mpg123' 'lib32-libldap')
conflicts=('deepin-wechat' 'deepin-wine-wechat')
install="deepin-wine-wechat.install"
_mirror="https://mirrors.aliyun.com/deepin"
source=("$_mirror/pool/non-free/d/deepin.com.wechat/deepin.com.wechat_${_deepinwechatver}_i386.deb"
  "reg.patch")
md5sums=('fe31cf4f0f6186fc1c99adc1512f5305'
  'f264f961704f2aa1d480971b0e58617a')

build() {
  msg "Extracting DPKG package ..."
  mkdir -p "${srcdir}/dpkgdir"
  tar -xvf data.tar.xz -C "${srcdir}/dpkgdir"
  sed "s/\(Categories.*$\)/\1Network;/" -i "${srcdir}/dpkgdir/usr/share/applications/deepin.com.wechat.desktop"
  msg "Extracting Deepin Wine WeChat archive ..."
  7z x -aoa "${srcdir}/dpkgdir/opt/deepinwine/apps/Deepin-WeChat/files.7z" -o"${srcdir}/deepinwechatdir"
  msg "Removing original outdated WeChat directory ..."
  rm -r "${srcdir}/deepinwechatdir/drive_c/Program Files/Tencent/WeChat"
  msg "Patching reg files ..."
  patch -p1 -d "${srcdir}/deepinwechatdir/" < "${srcdir}/reg.patch"
  msg "Creating font file link ..."
  ln -sf "/usr/share/fonts/wenquanyi/wqy-microhei/wqy-microhei.ttc" "${srcdir}/deepinwechatdir/drive_c/windows/Fonts/wqy-microhei.ttc"
  msg "Repackaging app archive ..."
  7z a -t7z -r "${srcdir}/files.7z" "${srcdir}/deepinwechatdir/*"
}

package() {
  msg "Preparing icons ..."
  install -d "${pkgdir}/usr/share"
  cp -a ${srcdir}/dpkgdir/usr/share/* "${pkgdir}/usr/share/"
  msg "Copying WeChat to /opt/deepinwine/apps/Deepin-WeChat ..."
  cp -r ${srcdir}/dpkgdir/opt ${pkgdir}/
}
