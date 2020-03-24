![test](https://github.com/metacpan/metacpan-web/workflows/test/badge.svg?branch=master)
[![Coverage Status](https://coveralls.io/repos/metacpan/metacpan-web/badge.svg)](https://coveralls.io/r/metacpan/metacpan-web)
[![Kritika Analysis Status](https://kritika.io/users/oalders/repos/4190324575950687/heads/master/status.svg)](https://kritika.io/users/oalders/repos/4190324575950687/heads/master/)

<!-- vim-markdown-toc GFM -->

* [Getting Started](#getting-started)
    * [Installing Manually](#installing-manually)
    * [Local Configuration Changes](#local-configuration-changes)
    * [Compatibility Notes](#compatibility-notes)

<!-- vim-markdown-toc -->

# Getting Started

We strongly recommend using [metacpan-docker](https://github.com/metacpan/metacpan-docker).
This will give you a virtual machine already configured and ready to start developing on.

## Installing Manually

If you prefer not to use Docker, the following commands will get you started:

    $ carton install
    $ npm install
    $ export PATH="$(realpath ./node_modules/.bin):$PATH"
    $ ./bin/prove t
    $ carton exec plackup -p 5001 -r

To run the tests in parallel, add `-j8` (or however many CPUs you have) to the
`prove` command.

## Local Configuration Changes

The back end defaults to `fastapi.metacpan.org`. Running a local API server is
optional and not required to hack on the front end.  The address to the API
being used can be changed in the `metacpan_web.conf` file.  Ideally you would create a
new file called `metacpan_web_local.conf` that contains

    api                 http://127.0.0.1:5000
    api_secure          http://127.0.0.1:5000
    api_external_secure http://127.0.0.1:5000

which will be loaded on top of the existing config file.

## Compatibility Notes

On Win32 (and possibly also on other platforms) when using Perl < 5.12, the
server started with plackup will generate warnings relating to date parsing.
These are caused by Plack due to a bug in the gmtime implementation and can be
removed by upgrading to Perl 5.12.
