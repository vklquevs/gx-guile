
# gx-guile

[Guile](//www.gnu.org/software/guile) hooks
for the [gx](//github.com/whyrusleeping/gx) package manager.

This script provides hooks to update Guile's module load path by scanning
the package's dependencies for other Guile packages.

## Installation
Copy or link the `gx-guile` script into `$PATH`.

## Usage
Create a new package:

```gx init --lang guile```

Enable `gx` packages somewhere before the first
`(use-modules (neato gx package) ...)` form:

```(load ".gx/gx.scm")```

Alternatively, invoke `guile` using `-l .gx/gx.scm ...`.

That's it. Everything else is as usual for gx.

### Packages considered for inclusion

Package dependencies are added to the load path if
they have a top-level `guile` object in `package.json`.
If it does not already exist:

```gx set --in-json .guile "{}"```

## Extra commands

```gx-guile set lib [dir]```

Set the module search path for this package to `dir`
(default `.`, i.e. the package's root directory).
Useful when a package organises modules into (e.g.) a `lib/` directory.

```gx-guile rebuild-module```

Regenerate `.gx/gx.scm` from gx dependencies.
This is done automatically after any package import or update.

## Issues
Nested package dependencies are untested - it assumes
that all packages are available as `gx/ipfs/$hash/$name`.

`.gx/gx.scm` is currently a hardcoded path.

## License
GPLv3

