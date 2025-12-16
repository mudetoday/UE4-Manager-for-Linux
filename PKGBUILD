# Maintainer: mudetoday <mudetoday@gmail.com>
pkgname=ue4-manager
pkgver=1.3
pkgrel=1
pkgdesc="This is an unofficial manager for the Unreal Engine 4"
arch=('any')
url="https://github.com/Liemaeu"
license=('GPL3')
depends=(
  'python'
  'python-pyqt5'
  'git'
  'nodejs'
  'npm'
  'base-devel'
  'xterm'
  'xdg-utils'
)
source=("$pkgname-$pkgver.tar.gz")
sha256sums=('SKIP')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"
  # Добавляем shebang в начало файла, если его нет
  if ! head -1 UE4_Manager.py | grep -q '^#!'; then
    sed -i '1i#!/usr/bin/env python3' UE4_Manager.py
  fi
  # Исправляем пути в скрипте для установки в /usr/share
  sed -i "s|loadUi(\"ue4|loadUi(\"/usr/share/$pkgname/ue4|g" UE4_Manager.py
  sed -i "s|QtGui.QIcon('Icon.png')|QtGui.QIcon('/usr/share/$pkgname/Icon.png')|g" UE4_Manager.py
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  # Устанавливаем основные файлы
  install -Dm755 UE4_Manager.py "$pkgdir/usr/bin/ue4-manager"
  install -Dm644 ue4-manager.ui "$pkgdir/usr/share/$pkgname/ue4-manager.ui"
  install -Dm644 ue4-installer.ui "$pkgdir/usr/share/$pkgname/ue4-installer.ui"
  install -Dm644 Icon.png "$pkgdir/usr/share/$pkgname/Icon.png"

  # Создаем .desktop файл для меню приложений
  install -Dm644 /dev/stdin "$pkgdir/usr/share/applications/ue4-manager.desktop" <<EOF
[Desktop Entry]
Name=UE4 Manager
Comment=GUI manager for Unreal Engine 4 on Linux
Exec=ue4-manager
Icon=/usr/share/ue4-manager/Icon.png
Terminal=false
Type=Application
Categories=Development;
EOF
}
