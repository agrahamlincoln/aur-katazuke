# Maintainer: Graham Rounds <email@example.com>
# This PKGBUILD is for personal use and is NOT published to aur.archlinux.org

pkgname=katazuke
pkgver=0.4.0
_commit=573e7d4
pkgrel=1
pkgdesc="Developer workspace maintenance tool for tidying up git repositories"
arch=('x86_64')
url="https://github.com/agrahamlincoln/katazuke"
license=('MIT')
depends=('git')
makedepends=('go')
options=(!debug)
source=("$pkgname-$pkgver.tar.gz::https://github.com/agrahamlincoln/$pkgname/archive/v$pkgver.tar.gz")
sha256sums=('8680b9585bdbd2ab0103716981d634db68eaf73387173d41f711f5dee92459e5')

build() {
    cd "$srcdir/$pkgname-$pkgver"

    export CGO_ENABLED=0
    export GOFLAGS="-buildmode=pie -trimpath -mod=readonly -modcacherw"

    go build \
        -ldflags "-s -w -X main.version=$pkgver -X main.commit=$_commit -X main.date=$(date -u +%Y-%m-%dT%H:%M:%SZ)" \
        -o "$pkgname" \
        ./cmd/katazuke
}

check() {
    cd "$srcdir/$pkgname-$pkgver"
    go test ./...
}

package() {
    cd "$srcdir/$pkgname-$pkgver"
    install -Dm755 "$pkgname" "$pkgdir/usr/bin/$pkgname"
    install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
    install -Dm644 README.md "$pkgdir/usr/share/doc/$pkgname/README.md"
}
