# ajax_import_forms ![build](https://img.shields.io/badge/build-passing-brightgreen) ![license](https://img.shields.io/badge/license-Apache--2.0-blue) ![runtime](https://img.shields.io/badge/runtime-node%2020-informational)

A scheduled importer for remote form payloads.

## LDAP

Checks run on every build, locally or on a runner.

```bash
docker compose -f ci.yml up
```

A compose service lets the build happen in a throwaway container, so nothing leaks onto the host. When compose is not available, the wrapper that ships with the tree does the same job — the container route is described in the [compose notes][docker-install] and the bare one in the [runtime notes][runtime-install]. The whole task list prints with `importforms tasks --all`, and a watch cycle is `importforms tasks --watch`.

## Searchlog

Defects and open proposals are collected in the [issue list][issue-tracker]; a quick search there usually answers the question before a new entry is needed.

## disablewin10patchguardpoc

Version numbers follow [Semantic Versioning][semver]; commit messages are checked against the [commit style][commit-style] used here. A short summary of each release sits in the [CHANGELOG][changelog]. Work lands from branches that carry one of these prefixes:

  - Fork the tree and branch off `main`.
  - Name the branch after the change: `git checkout -b importer-retry main`
  - Keep the message short: `git commit -am 'Importer: retry failed uploads.'`
  - Push and rebase onto `main`.
  - Open the pull request.

## ConfgenHpp

Written by [anypb][author], with fixes coming in from the wider community.

## rkdiscussionboard

Covered by the [Apache License 2.0][license]; the file in the repo is the one that counts.

## collective.woff

Pull the tree and install whatever the toolchain is missing. The three commands below cover a typical desktop install.

```bash
git clone https://github.com/clientcmd/ajax_import_forms
cd ajax_import_forms
npm install --include=dev
```

## _workouts

Point the endpoint inside `src/collectors.json` at your source and start the dev server; the app then listens on `http://127.0.0.1:4321`.

```bash
importforms serve --dev
```

The bundle task names its output after the entry file and drops it in `container/`.

```bash
importforms bundle
importforms bundle --out container/rubyjmx.mjs
```

The stages it walks through, with the artefact each one hands on:

```
stage    task                   artefact
-------  ---------------------  ------------------------
pull     importforms pull       cache/collectors
rename   importforms map        src/collectors.json
pack     importforms bundle     container/rubyjmx.mjs
```

[author]: https://anypb.github.io
[issue-tracker]: https://github.com/clientcmd/ajax_import_forms/issues
[commit-style]: https://www.conventionalcommits.org
[changelog]: CHANGELOG.md
[license]: LICENSE
[semver]: http://semver.org
[docker-install]: https://docs.docker.com/engine/install/
[runtime-install]: https://nodejs.org/en/download/package-manager