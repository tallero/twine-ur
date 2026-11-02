# SPDX-License-Identifier: AGPL-3.0

#    -----------------------------------------------------
#    Copyright © 2024, 2025, 2026  Pellegrino Prevete
#
#    All rights reserved
#    -----------------------------------------------------
#
#    This program is free software: you can redistribute
#    it and/or modify it under the terms of the
#    GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it
#    will be useful, but WITHOUT ANY WARRANTY;
#    without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
#    See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the
#    GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Felix Yan
#     <felixonmars@archlinux.org>
#   Chris Warrick
#     <aur@chriswarrick.com>

if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
if [[ ! -v "_git" ]]; then
  _git="true"
fi
if [[ ! -v "_ns" ]]; then
  _ns="pypa"
  _ns="themartiancompany"
fi
_py="python"
_pkg=twine
pkgbase="${_pkg}"
pkgname=(
  "${_pkg}"
)
pkgver=7.0.0
pkgrel=1
pkgdesc='Collection of utilities for interacting with PyPI'
arch=(
  "any"
)
_http="https://${_git_service}.com"
url="${_http}/${_ns}/${_pkg}"
_url="${url}"
license=(
  "Apache-2.0"
)
depends=(
 "${_py}"
 "${_py}-packaging"
 "${_py}-readme-renderer"
 "${_py}-requests"
 "${_py}-requests-toolbelt"
 "${_py}-urllib3"
 "${_py}-importlib-metadata"
 "${_py}-keyring"
 "${_py}-rfc3986"
 "${_py}-rich"
 "${_py}-id"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
  "${_py}-setuptools-scm"
  "${_py}-wheel"
)
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
checkdepends=(
  "git"
  "${_py}-munch"
  "${_py}-jaraco.envs"
  "${_py}-portend"
  "${_py}-pretend"
  "${_py}-pytest-services"
  "${_py}-pytest-socket"
)
provides=(
  "${_py}-twine=${pkgver}"
)
conflicts=(
  "${_py}-${_pkg}"
)
replaces=(
  "${_py}-${_pkg}"
)
_tarname="${_pkg}"
_src="${_tarname}::git+${_url}.git#tag=${pkgver}"
source=(
  "${_src}"
)
sha512sums=(
  '644c900f1cc772b941196c0e42d7d44de7b6495e0381a7f24a98b85bdb622d48006f666b962a33defcf482c8d4c5848e8c72b122506a9ed737f278faae1f2699'
)
b2sums=(
  'c6405482e9d9ba55e3b55604a5c8d69951d8c6d6131e95fd32c2494cebfbcf30de2ca25dd46e5557cd7f2b27681ad19a0020ed2b556d1c52aa886c24ef0c2461'
)

build() {
  cd \
    "${_tarname}"
  SETUPTOOLS_SCM_PRETEND_VERSION="${pkgver}" \
  "${_py}" \
    -m \
      "build" \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_tarname}"
  # Ignored tests are copied from upstream tox.ini:
  # https://github.com/pypa/twine/blob/4.0.2/tox.ini#L16
  "${_py}" \
    -m \
      "pytest" \
    --ignore-glob \
    '*integration*.py'
}

package() {
  cd \
    "${_tarname}"
  "${_py}" \
    -m \
      "installer" \
    --destdir="${pkgdir}" \
    "dist/"*".whl"
  # create symlink
  ln \
    -s \
    "${_pkg}" \
    "${pkgdir}/usr/bin/${_pkg}3"
}
