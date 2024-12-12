# Maintainer: devome <evinedeng@hotmail.com>

_pkgname="wechat"
pkgname="${_pkgname}-bin"
pkgver=4.0.1.7
pkgrel=1
pkgdesc="WeChat from Tencent | 微信官方版"
arch=("x86_64" "aarch64" "loong64")
url="https://linux.weixin.qq.com"
license=("custom:Software License and Service of Tencent Weixin")
provides=("${_pkgname}"{,-universal})
conflicts=("${_pkgname}"{,-universal})
replaces=("${_pkgname}-universal"{,-privilege})
depends=(at-spi2-core jack libpulse libxcomposite libxdamage libxkbcommon-x11 libxrandr mesa nss pango xcb-util-image xcb-util-keysyms xcb-util-renderutil xcb-util-wm)
optdepends=("noto-fonts-cjk: Chinese font support"
            "noto-fonts-emoji: emoji support")
source=("LICENSE-zh_CN.html::https://weixin.qq.com/agreement?lang=zh_CN"
        "LICENSE-zh_HK.html::https://weixin.qq.com/agreement?lang=zh_HK"
        "LICENSE-zh_TW.html::https://weixin.qq.com/agreement?lang=zh_TW"
        "LICENSE-en.html::https://www.wechat.com/mobile/en/service_terms.html")
source_x86_64=("local://${_pkgname}-${pkgver}-x86_64.deb")
source_aarch64=("local://${_pkgname}-${pkgver}-aarch64.deb")
source_loong64=("local://${_pkgname}-${pkgver}-loong64.deb")
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP')
sha256sums_x86_64=('88ea106a68fac96bc17c4209f856f45fa13e105625dc49cf8644d1b2d882f7a9')
sha256sums_aarch64=('6758c8b1f9a42c2dbd5a96332139ace2cf999ec1bc00994adac880559a9f997f')
sha256sums_loong64=('598e89861688fe48ce6342ebc3ec9ea3c3306aad0e8ba4b3c86413931b327eba')
noextract=("${_pkgname}-${pkgver}-"{x86_64,aarch64,loong64}.deb)
options=("!strip")

prepare() {
    bsdtar -xOf "${_pkgname}-${pkgver}-${CARCH}.deb" data.tar.xz | bsdtar -xmf- --exclude usr/share/doc
    sed -e "s|^Icon=.*|Icon=${_pkgname}|" \
        -e "s|^Categories=.*|Categories=Network;InstantMessaging;Chat;|" \
        -e "s|^Exec=.*|Exec=env 'QT_QPA_PLATFORM=wayland;xcb' QT_AUTO_SCREEN_SCALE_FACTOR=1 /usr/bin/${_pkgname} %U|" \
        -i "usr/share/applications/${_pkgname}.desktop"
}

package() {
    mv {opt,usr} "${pkgdir}"
    ln -s "/opt/${_pkgname}/${_pkgname}" "${pkgdir}/usr/bin/${_pkgname}"
    install -Dm644 LICENSE-* -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
