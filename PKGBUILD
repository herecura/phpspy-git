# Maintainer: BlackIkeEagle <ike DOT devolder AT gmail DOT com>

_gitname=phpspy
pkgname=phpspy-git
pkgver=20200110.33cbc6f
pkgrel=1
pkgdesc="low-overhead sampling profiler for PHP 7"
arch=('x86_64')
url="https://github.com/adsr/phpspy"
depends=('glibc' 'perl')
makedepends=('python' 'git')
license=('MIT')
source=(
    "$_gitname::git://github.com/adsr/phpspy.git"
    "phpspy-flamegraph"
)
sha512sums=('SKIP'
            '1e79a9a7f242ab1520372111206737e1f44c20a69989fb1e00f732a2ee74f8b8e1ec9d711800580defc5a2b3add7273928a39661c8b257d43dfa84363c2aed4d')

pkgver() {
    cd "$_gitname"
    git log -1 --date=short --format="%cd.%h" | tr -d '-'
}

prepare() {
    cd "$_gitname"
    sed -e '/libpthread/d' -i Makefile
}

build() {
    cd "$_gitname"
    make
}

package() {
    cd "$_gitname"
    install -Dm 755 phpspy "$pkgdir/usr/bin/phpspy"

    # install flamegraph helper
    install -Dm 755 "$srcdir/phpspy-flamegraph" \
        "$pkgdir/usr/bin/phpspy-flamegraph"

    # install helper scripts for flamegraph
    install -Dm 755 stackcollapse-phpspy.pl \
        "$pkgdir/usr/lib/phpspy/stackcollapse-phpspy.pl"
    install -Dm 755 vendor/flamegraph.pl \
        "$pkgdir/usr/lib/phpspy/flamegraph.pl"

    # license
    install -dm755 "$pkgdir/usr/share/licenses/$pkgname"
    install -Dm644 LICENSE \
        "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
