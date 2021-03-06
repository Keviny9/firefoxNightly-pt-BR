# Maintainer: Keviny Gabriel  <kevinydutra@gmail.com>
# Contributor: Keviny Gabriel 
_name=firefox
_channel=nightly
_lang=pt-BR
#_version=69.0a1
_version=70.0a1
pkgname=${_name}-${_channel}
#pkgver=69.0a1.
pkgver=70.0a1.
pkgrel=1
pkgdesc="Navegador independente da Mozilla - Nightly build (pt-BR)"
arch=('i686' 'x86_64')
url="https://www.mozilla.org/pt-BR/firefox/nightly"
depends=('dbus-glib' 'gtk3' 'libxt' 'nss' 'mime-types')
optdepends=('pulseaudio: audio support'
            'ffmpeg: h.264 video'
            'hunspell: spell checking'
            'hyphen: hyphenation'
            'libnotify: notification integration'
            'networkmanager: location detection via available WiFi networks'
            'speech-dispatcher: text-to-speech'
            'startup-notification: support for FreeDesktop Startup Notification')
_url="https://ftp.mozilla.org/pub/firefox/nightly/latest-mozilla-central-l10n"
_src="${_name}-${_version}.${_lang}.linux"
_filename="$(date +%Y%m%d)-${_src}"
license=("GPL" "MPL" "LGPL")
source=("${pkgname}.desktop" 'policies.json')
source_i686=("${_filename}-i686.tar.bz2"::"${_url}/${_src}-i686.tar.bz2"
             "${_filename}-i686.tar.bz2.asc"::"${_url}/${_src}-i686.tar.bz2.asc"
             "${_filename}-i686.checksums"::"${_url}/${_src}-i686.checksums")
source_x86_64=("${_filename}-x86_64.tar.bz2"::"${_url}/${_src}-x86_64.tar.bz2"
               "${_filename}-x86_64.tar.bz2.asc"::"${_url}/${_src}-x86_64.tar.bz2.asc"
               "${_filename}-x86_64.checksums"::"${_url}/${_src}-x86_64.checksums")

 sha512sums=('42426e7b510bd88cbf7b246bf66d7768afa5d71389bf15f7a4231dc24f99fd73284dd9a0a8eb4342b42337c2c7dd843e570a93afa7d3b44c97ecbf5e38e433ac'
            '5ed67bde39175d4d10d50ba5b12063961e725e94948eadb354c0588b30d3f97d2178b66c1af466a6e7bd208ab694227a1391c4141f88d3da1a1178454eba5308')

# sha512sums=('e1ac6ad19515d7d23f869da2ab0245bb6f9a3488ca7fd50d634d0c93c64974d364b234c59c25e17179de1d9af37ebec2de7ae1cbb063c0b1888289feeca71238'
#            '6ef18f55dd93eb52471d03f4fda53d5ddac3f984ac0c8303fe6a6a34d093cfb1014a7a8394f42e32abb305f5c0ac6ce9f448ec721c698e06e13964289388ca8e')
sha512sums_i686=('SKIP' 'SKIP' 'SKIP')
sha512sums_x86_64=('SKIP' 'SKIP' 'SKIP')
 validpgpkeys=('14F26682D0916CDD81E37B6D61B7B526D98F0353') # Mozilla’s GnuPG release keymd5sums=("md5sum do source")

# validpgpkeys=('') # Mozilla’s GnuPG release keymd5sums=("md5sum do source")


pkgver() {
  echo "${_version}.$(head -n1 ${_filename}-${CARCH}.txt | cut -c-8)"
}

package() {
  OPT_PATH="opt/${pkgname}"

  # Install the package files
  install -d "${pkgdir}"/{usr/bin,opt}
  cp -r ${_name} "${pkgdir}"/${OPT_PATH}
  ln -s "/${OPT_PATH}/${_name}" "${pkgdir}"/usr/bin/${pkgname}

  # Install .desktop files
  #install -Dm644 "${srcdir}"/${pkgname}.desktop -t "${pkgdir}"/usr/share/applications
  install -Dm644 "${srcdir}"/${pkgname}.desktop -t "${pkgdir}"/usr/share/applications

  # Install icons
  SRC_LOC="${srcdir}"/${_name}/browser
  DEST_LOC="${pkgdir}"/usr/share/icons/hicolor
  for i in 16 32 48 64 128
  do
      install -Dm644 "${SRC_LOC}"/chrome/icons/default/default${i}.png "${DEST_LOC}"/${i}x${i}/apps/${pkgname}.png
  done

  # Disable auto-updates
  install -Dm644 "${srcdir}"/policies.json -t "${pkgdir}"/${OPT_PATH}/distribution

  # Use system-provided dictionaries
  rm -rf "${pkgdir}"/${OPT_PATH}/{dictionaries,hyphenation}
  ln -sf /usr/share/hunspell "${pkgdir}"/${OPT_PATH}/dictionaries
  ln -sf /usr/share/hyphen "${pkgdir}"/${OPT_PATH}/hyphenation
}
