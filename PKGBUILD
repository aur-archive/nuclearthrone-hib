# Maintainer: Duncan K. <duncank@fastmail.fm>

pkgname=nuclearthrone-hib
pkgver=0_20140617
pkgrel=1
pkgdesc='Vlambeers latest action roguelike-like about mutants that spend their workdays trying to fight for the throne in a post-apocalyptic world (Humble Bundle version)'
url='http://www.nuclearthrone.com/'
arch=('i686' 'x86_64')
license=('custom:commercial')
makedepends=('unrar')
if [ $CARCH == i686 ]; then
  depends=('libgl' 'glu' 'openal' 'openssl')
  optdepends=('libpulse: PulseAudio support')
else
  depends=('lib32-libgl' 'lib32-glu' 'lib32-openal' 'lib32-openssl')
  optdepends=('lib32-libpulse: PulseAudio support')
fi
options=('!strip' '!upx')
PKGEXT='.pkg.tar.gz'
DLAGENTS+=('hib::/usr/bin/echo "Could not find %u. Manually download it to \"$(pwd)\", or set up a hib:// DLAGENT in /etc/makepkg.conf."; exit 1')
_installer='NuclearThrone_j16linux.rar'
noextract=($_installer)

source=("hib://${_installer}"
        "nuclearthrone.desktop")
md5sums=('3945577de1ba1cfcb47a702f209eb0e8'
         '61df1e4310d51ff44b339cbb171a9e57')

package() {
  cd $srcdir
  _installdir="/opt/nuclearthrone"; _target="${pkgdir}/${_installdir}"

  # Extract and fix execute permission
  unrar x -o+ $_installer
  chmod a+x "${srcdir}/linux/runner"

  # Install game files
  mkdir -p $_target
  cp -rT "linux" $_target

  # Install desktop entry
  install -Dm644 "nuclearthrone.desktop" \
                 "${pkgdir}/usr/share/applications/Nuclear Throne.desktop"

  # Install icon
  install -Dm644 "linux/assets/icon.png" \
                 "${pkgdir}/usr/share/pixmaps/nuclearthrone.png"

  # Link executable
  install -d "${pkgdir}/usr/bin"
  ln -s "${_installdir}/runner" "${pkgdir}/usr/bin/nuclearthrone"
}
