pkgname=steam-headless
pkgdesc="Online steam play"
pkgver=1.0.0
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
    'sysuser.conf'
)
sha256sums=('75f5932b2e3c7877c85da00c04b1d2522465ee6878440cc9975d8242fcc8aae6'
            '26b7df0d319a049f5168fc09232fd02d90c3d1f39d645f89099a28271cdfe9de'
            'd5c5566b929668592aeeec01f047e04f75cb73242afe564cb64069d9a8a5f133'
            'e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855'
            '39b825d3f28a6720a007c09be3874c08ba623d30676703a8e056fc458319a771'
            '59df9e60f2e7c49ffa59e9daf7a251819b68f934312d33de8f31ac13821a75e7'
            '8c3ac9d1332146a20f25f63fc8d02af76213477919daa06fa0a93bb8d3d37bd3')
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
    install -D -m644 sysuser.conf $pkgdir/usr/lib/sysusers.d/${pkgname}.conf
}