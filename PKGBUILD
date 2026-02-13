# Maintainer: Graham Rounds <email@example.com>
# This PKGBUILD is for personal use and is NOT published to aur.archlinux.org

pkgname=katazuke
pkgver=0.8.0
_commit=5490b26
pkgrel=1
pkgdesc="Developer workspace maintenance tool for tidying up git repositories"
arch=('x86_64')
url="https://github.com/agrahamlincoln/katazuke"
license=('MIT')
depends=('git')
makedepends=('go')
options=(!debug)
source=("$pkgname-$pkgver.tar.gz::https://github.com/agrahamlincoln/$pkgname/archive/v$pkgver.tar.gz")
sha256sums=('746c0fe6927742906bab7ba977652261152fed506c624e6e29e5cec72c2d2b63')

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
