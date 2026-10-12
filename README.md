# go-scikit.github.io

The go-scikit portal (Hugo), served at <https://go-scikit.github.io/>: the
stack, one card per member organisation with its site and documentation, the
measured claims with links to their evidence, and a first notebook.

The design is the go-* family landing kit, imported as the Hugo module
[go-fleettools/landingkit](https://github.com/go-fleettools/landingkit)
(pinned in `go.mod`; `kit.go` keeps `go mod tidy` from dropping it). The only
thing set here is `[params.brand]` in `hugo.toml`, written by
`landingkit brand static/img/logo.svg` from the logo's gradient. The member
organisations, the claims and the repositories are lists in `hugo.toml`; the
page is `layouts/index.html`.

The notebook is real: the hero shows `example/first.md` and, under it,
`example/output.txt`, both read at build time. `example/go.mod` pins the
libraries it imports and the `notebook` command (as a `tool`), and the `ci`
workflow runs it again and fails if the output differs.

```sh
cd example && go tool notebook run first.md | sed -E 's/, (ran in [^)]*|kept)\)/)/' > output.txt
hugo server
```

| Workflow | What |
| --- | --- |
| `hugo.yml` | builds on pull requests; builds and deploys to Pages on `main` |
| `ci.yml` | the site builds and names every member organisation and repository; the notebook prints what the page says |
| `links.yml` | every link and image of the built site resolves (`landingkit links`) |

BSD-3-Clause.
