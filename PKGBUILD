# Maintainer: devome <evinedeng@hotmail.com>

_pkgname="wechat"
pkgname="${_pkgname}-bin"
pkgver=4.0.1.3
pkgrel=1
pkgdesc="WeChat from Tencent | 微信官方版"
arch=("x86_64" "aarch64" "loong64")
url="https://linux.weixin.qq.com"
license=("custom:Software License and Service of Tencent Weixin")
provides=("${_pkgname}"{,-universal})
conflicts=("${_pkgname}"{,-universal})
replaces=("${_pkgname}"{,-universal{,-privilege}})
depends=(at-spi2-core jack libpulse libxcomposite libxdamage libxkbcommon-x11 libxrandr mesa nss pango xcb-util-image xcb-util-keysyms xcb-util-renderutil xcb-util-wm)
makedepends=("patchelf")
optdepends=("noto-fonts-cjk: Chinese font support" "noto-fonts-emoji: emoji support")
source=("LICENSE-zh_CN.html::https://weixin.qq.com/agreement?lang=zh_CN"
        "LICENSE-zh_HK.html::https://weixin.qq.com/agreement?lang=zh_HK"
        "LICENSE-zh_TW.html::https://weixin.qq.com/agreement?lang=zh_TW"
        "LICENSE-en.html::https://www.wechat.com/mobile/en/service_terms.html")
source_x86_64=("local://${_pkgname}-${pkgver}-x86_64.deb")
source_aarch64=("local://${_pkgname}-${pkgver}-aarch64.deb")
source_loong64=("local://${_pkgname}-${pkgver}-loong64.deb")
sha256sums=('SKIP' 'SKIP' 'SKIP' 'SKIP')
sha256sums_x86_64=('6038190f01155d285bcc7f7fe13772708b5d7310298c162279b9b96d75a10e06')
sha256sums_aarch64=('c8769ff8ed855e04e40aedebe703a95264cae30a1c0ef4789c52c80de2da8a44')
sha256sums_loong64=('3f9ac4e84b345a4d1dc76af01328619d7debea1b3d49d7138f3f7534d8989a99')
noextract=("${_pkgname}-${pkgver}-"{x86_64,aarch64,loong64}.deb)
options=("!strip")

prepare() {
    bsdtar -xOf "${_pkgname}-${pkgver}-${CARCH}.deb" data.tar.xz | bsdtar -xmf- --exclude usr/share/doc
    find "opt/${_pkgname}/vlc_plugins" -type f | xargs -I {} patchelf --set-rpath '${ORIGIN}:${ORIGIN}/../..' {}
    sed -e "s|^Icon=.*|Icon=${_pkgname}|" \
        -e "s|^Categories=.*|Categories=Network;InstantMessaging;Chat;|" \
        -e "s|^Exec=.*|Exec=env 'QT_QPA_PLATFORM=wayland;xcb' QT_AUTO_SCREEN_SCALE_FACTOR=1 /usr/bin/${_pkgname} %U|" \
        -i "usr/share/applications/${_pkgname}.desktop"
}

package() {
    if [[ ${CARCH} == loong64 ]]; then
        depends_loong64+=(liblol)
    fi
    mv {opt,usr} "${pkgdir}"
    ln -s "/opt/${_pkgname}/${_pkgname}" "${pkgdir}/usr/bin/${_pkgname}"
    install -Dm644 LICENSE-* -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
