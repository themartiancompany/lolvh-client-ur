# SPDX-License-Identifier: AGPL-3.0

#    ------------------------------------------------------------
#    Copyright © 2023, 2024, 2025, 2026
#                Pellegrino Prevete
#
#    All rights reserved
#    ------------------------------------------------------------
#
#    This program is free software: you can redistribute it
#    and/or modify it under the terms of the GNU Affero General
#    Public License as published by the Free Software Foundation,
#    either version 3 of the License, or (at your option) any
#    later version.
#
#    This program is distributed in the hope that it will be
#    useful, but WITHOUT ANY WARRANTY; without even the implied
#    warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR
#    PURPOSE. See the GNU Affero General Public License for
#    more details.
#
#    You should have received a copy of the GNU Affero General
#    Public License along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainer:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>

_os="$(
  uname \
    -o)"
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
  _git_http_host="gitlab"
fi
if [[ ! -v "_git_http_host" ]]; then
  _git_http_host="${_git_service}"
fi
if [[ ! -v "_ns" ]]; then
  _ns="themartiancompany"
fi
if [[ ! -v "_tag_name" ]]; then
  _tag_name="commit"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_service}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _archive_format="zip"
      elif [[ "${_tag_name}" == "pkgver" ]]; then
        _archive_format="tar.gz"
      fi
    elif [[ "${_git_service}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    else
      _archive_format="tar.gz"
    fi
  fi
fi
_solc="true"
_hardhat="true"
_py="python"
_pkg=lolvh-client
pkgbase="${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver="0.0.0.0.0.0.0.0.0.0.0.0.1.1"
_commit="8bb75f3ff6b2de72d703e3768366cf51ab66900e"
pkgrel=1
_pkgdesc=(
  "Simple OVHCloud DNS client using"
  "the Python OVH module."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://${_git_http_host}.com"
_ns="themartiancompany"
url="${_http}/${_ns}/${pkgname}"
license=(
  'AGPL3'
)
depends=(
  "libcrash-bash"
  "${_py}"
  "${_py}-ovh"
)
provides=(
  "${_py}-${_pkg}=${pkgver}"
)
optdepends=()
if [[ "${_os}" != "GNU/Linux" ]] && \
   [[ "${_os}" == "Android" ]]; then
  depends+=(
  )
  optdepends+=(
  )
fi
optdepends+=(
)
makedepends=(
  'make'
  "${_py}-docutils"
)
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
fi
checkdepends=(
  "shellcheck"
)
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
_gitlab_sum=""
_gitlab_sig_sum=""
_github_sum=""
_github_sig_sum=""
if [[ "${_git_service}" == "gitlab" ]]; then
  _sum="${_gitlab_sum}"
  _sig_sum="${_gitlab_sig_sum}"
elif [[ "${_git_service}" == "github" ]]; then
  _sum="${_github_sum}"
  _sig_sum="${_github_sig_sum}"
fi
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_evmfs_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_sum}"
_evmfs_src="${_tarname}.tar.gz::${_evmfs_uri}"
_sig_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_sig_sum}"
_sig_src="${_tarname}.tar.gz.sig::${_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    echo \
      "ahah"
    exit \
      1
  elif [[ "${_git}" == "false" ]]; then
    _src="${_evmfs_src}"
    _sum="${_sum}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_sig_sum}"
    )
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == true ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    if [[ "${_tag_name}" == 'pkgver' ]]; then
      _src="${_tarname}.tar.gz::${_url}/archive/refs/tags/${_tag}.tar.gz"
      _sum="SKIP"
    elif [[ "${_tag_name}" == "commit" ]]; then
      if [[ "${_git_http_host}" == "github" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
      elif [[ "${_git_http_host}" == "gitlab" ]]; then
        _uri="${_url}/-/archive/${_commit}/${_tarname}.${_archive_format}"
      fi
      _src="${_tarname}.${_archive_format}::${_uri}"
    fi
  fi
fi
source=(
  "${_src}"
)
sha256sums=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  'DD6732B02E6C88E9E27E2E0D5FC6652B9D9A6C01'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

check() {
  cd \
    "${_tarname}"
  make \
    -k \
    check
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    PREFIX="/usr"
    DESTDIR="${pkgdir}"
  )
  cd \
    "${_tarname}"
  make \
    "${_make_opts[@]}" \
    install
  install \
    -Dm644 \
    "COPYING" \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgbase}-docs/"
}

# vim: ft=sh syn=sh et
