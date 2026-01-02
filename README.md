
# `installer`

Quickly install pre-compiled binaries from Github releases.

Installer is an HTTP server which returns shell scripts. The returned script will detect platform OS and architecture, choose from a selection of URLs, download the appropriate file, un(zip|tar|gzip) the file, find the binary (largest file) and optionally move it into your `PATH`. Useful for installing your favourite pre-compiled programs on hosts using only `curl`.

[![GoDev](https://img.shields.io/static/v1?label=godoc&message=reference&color=00add8)](https://pkg.go.dev/github.com/voluzi/installer)
[![CI](https://github.com/voluzi/installer/workflows/CI/badge.svg)](https://github.com/voluzi/installer/actions?workflow=CI)

## Usage

```sh
curl https://get.voluzi.com/<repo>@<release>! | bash
```

*Or you can use* `wget -qO- <url> | bash`

## Examples

```sh
# Install latest cosmoseed
curl https://get.voluzi.com/cosmoseed! | bash

# Install specific version of cosmoguard
curl https://get.voluzi.com/cosmoguard@v1.0.0! | bash

# Download to current directory (without !)
curl https://get.voluzi.com/cosmoseed | bash
```

**Path API**

* `repo` Github repository (**required**)
* `release` Github release name (defaults to the **latest** release)
* `!` When provided, downloads binary directly into `/usr/local/bin/` (defaults to working directory)

**Query Params**

* `?insecure=1` Force `curl`/`wget` to skip certificate checks
* `?as=` Force the binary to be named as this parameter value
* `?os=` Explicit set OS (ignore system OS)
* `?arch=` Explicit set architecture (ignore system arch)

## Security

:warning: You're right to be wary of piping shell scripts from unknown servers. You can leave off `| bash` and review the script yourself first.

## Private repos

Set `GITHUB_TOKEN` on both your server (instance of `installer`) and client (before you run `curl https://get.voluzi.com/<repo> | bash`)

## Host your own

* Install from source

    ```sh
    go install github.com/voluzi/installer@latest
    ```

## Configuration

Environment variables:

* `FORCE_USER` - Lock installer to a single GitHub user
* `FORCE_REPO` - Lock installer to a single GitHub repo
* `BINARY_RENAME` - Rename binaries (format: `repo:name,repo2:name2`)
* `GITHUB_TOKEN` - GitHub API token for private repos

#### MIT License

Copyright © 2020 Jaime Pillora &lt;dev@jpillora.com&gt;

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
