pkgname=steam-headless
pkgdesc="Online steam play"
pkgver=2.0.1
pkgrel=1
arch=('x86_64')
url="https://github.com/p1x3l101-10/"
licence=('none')
depends=('podman')
_quadlets=(
    'steam.container'
    'steam.image'
)
_units=(
    'steam.target'
)
source=(
    "${_quadlets[@]}"
    "${_units[@]}"
    'config.env'
    'config-system.env'
    'tmpfiles.conf'
)
sha256sums=('db2ee89bdb627aab7763a53fe01d156e4a47e27d696c222b8ffffb370633a49c'
            'aab2a270413f5dbc4e1074d725d8ba7496883e5cf96281788294011fe8422b7f'
            'd5c5566b929668592aeeec01f047e04f75cb73242afe564cb64069d9a8a5f133'
            'e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855'
            '68470c93f2061dba5b60d846be4556aba4348ce655d821c9709617c879a16cca'
            'c75ad7c7f04bf421beba55bfa35fa6d601760510ee8b52f01af8a2d593565368')
options=("!purge") # I use .pod files, and purge removes them. Also there is nothing to purge here anyways

package() {
    for quadlet in "${_quadlets[@]}"; do
        install -D -m644 $quadlet $pkgdir/usr/share/containers/systemd/$quadlet
    done
    for unit in "${_units[@]}"; do
        install -D -m644 $unit $pkgdir/usr/lib/systemd/system/$unit
    done
    for config in "config"; do
        install -D -m644 $config.env $pkgdir/usr/share/factory/etc/${pkgname}/$config.env
        install -D -m644 $config-system.env $pkgdir/usr/lib/${pkgname}/$config.env
    done
    install -D -m644 tmpfiles.conf $pkgdir/usr/lib/tmpfiles.d/${pkgname}.conf
}