# Maintainer: Eugene Nikolsky <pluton dot od at gmail dot com>

pkgname=pitz-git
pkgver=20120321
pkgrel=2
pkgdesc="Open-source, distributed, plain-text, command-line, very flexible issue tracker (inspired by ditz)"
arch=('any')
license=('BSD')
url="https://github.com/mw44118/pitz"
depends=('python2' 'python2-tempita' 'python2-jinja' 'python2-yaml' 'python2-clepy' 'python2-docutils' 'python2-decorator')
optdepends=('ipython2: for pitz-shell')
makedepends=('git')
source=('ipython-0.11.patch')
md5sums=('18f84d49b73fcc1610feccea01941eec')

_gitroot='git://github.com/mw44118/pitz.git'
_gitname=$pkgname

build()
{
  cd "${srcdir}"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone --depth=1 "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  cp -r "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  patch -p1 -i $srcdir/ipython-0.11.patch

  python2 setup.py install --root="${pkgdir}" --optimize=1 || return 1
  install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -D -m644 bash_completion.bash "${pkgdir}/etc/bash_completion.d/pitz"
}

