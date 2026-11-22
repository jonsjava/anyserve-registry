# Anyserve registry

The signed main registry for [Anyserve](https://github.com/jonsjava/anyserve),
served from GitHub Pages at:

```
https://jonsjava.github.io/anyserve-registry/index.json
https://jonsjava.github.io/anyserve-registry/index.json.sig
```

`anyserve refresh` downloads these files. It uses the index only if
`index.json.sig` is a valid Ed25519 signature over the exact bytes of
`index.json`, made with the key pinned in Anyserve:

```
anyserve-ed25519:6dJrvi7OZIf0qcvUcX0ZoPv6b+RyRSFWjTtOLRrMYOE=
```

## Don't edit these files

The index is built from the definitions in
[anyserve/registry/services](https://github.com/jonsjava/anyserve/tree/main/registry/services).
Changing them here by hand breaks the signature, and Anyserve rejects
the index. To add or fix a service, open a pull request on the main
repository; see its
[CONTRIBUTING.md](https://github.com/jonsjava/anyserve/blob/main/CONTRIBUTING.md).

A new index is published automatically when definition changes are merged
into the main repository, by its
[Publish registry workflow](https://github.com/jonsjava/anyserve/blob/main/.github/workflows/publish-registry.yml).

## Check the signature yourself

```bash
curl -sO https://jonsjava.github.io/anyserve-registry/index.json
curl -sO https://jonsjava.github.io/anyserve-registry/index.json.sig
go run github.com/jonsjava/anyserve/tools/regbuild@latest -verify index.json \
  -pub anyserve-ed25519:6dJrvi7OZIf0qcvUcX0ZoPv6b+RyRSFWjTtOLRrMYOE=
```
