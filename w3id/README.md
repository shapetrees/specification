# w3id.org/shapetrees

[`.htaccess`](.htaccess) is the redirect configuration for the
`https://w3id.org/shapetrees` namespace. It is kept here so it is versioned
alongside the vocabulary it resolves, but w3id.org serves it from a separate
repository — a copy in this repo has no effect on its own.

## Installing it

The namespace is already registered, as
[`shapetrees/`](https://github.com/perma-id/w3id.org/tree/master/shapetrees) in
[perma-id/w3id.org](https://github.com/perma-id/w3id.org), listing
[@ericprud](https://github.com/ericprud),
[@justinwb](https://github.com/justinwb) and
[@elf-pavlik](https://github.com/elf-pavlik) as maintainers. The entry as
registered sends *every* path to the raw `shapetrees.ttl` on GitHub, which is
right for the vocabulary but leaves the documents unreachable.

To install the rules here, fork `perma-id/w3id.org`, replace
`shapetrees/.htaccess` with this one, and open a pull request. Whenever a rule
changes it has to be sent there again — nothing syncs automatically.

## What it resolves

| Request | Redirects to |
| --- | --- |
| `https://w3id.org/shapetrees` with an RDF `Accept` header | `https://shapetrees.github.io/specification/shapetrees.ttl` |
| `https://w3id.org/shapetrees` from a browser | `https://shapetrees.github.io/shapetrees.org/` |
| `https://w3id.org/shapetrees/TR/specification/` | `https://shapetrees.github.io/specification/` |
| `https://w3id.org/shapetrees/TR/primer/` | `https://shapetrees.github.io/primer/` |
| anything else under `/shapetrees/` | the same path on `https://shapetrees.github.io/shapetrees.org/` |

Two changes from the registered entry are worth calling out. The vocabulary is
served from GitHub Pages rather than `raw.githubusercontent.com`, so it arrives
as `text/turtle` instead of `text/plain`. And it is only served to clients that
ask for RDF: a browser following `https://w3id.org/shapetrees` now lands on the
Shape Trees home page rather than downloading a Turtle file.

The redirects are `302` so the GitHub Pages hosts can be moved later without
poisoning caches. Once the arrangement has settled, they can become `301`.

## Testing a change

`.htaccess` cannot be tested by opening it locally; run it under Apache with
`mod_rewrite`:

```bash
docker run --rm -p 8080:80 \
  -v "$PWD/.htaccess:/usr/local/apache2/htdocs/shapetrees/.htaccess" \
  httpd:2.4 \
  sh -c "sed -i 's/^#LoadModule rewrite_module/LoadModule rewrite_module/; s|AllowOverride None|AllowOverride All|' conf/httpd.conf && httpd-foreground"
```

then check that each row of the table above lands where it should:

```bash
curl -sI -H 'Accept: text/turtle' http://localhost:8080/shapetrees/ | grep -i location
curl -sI http://localhost:8080/shapetrees/TR/specification/ | grep -i location
curl -sI http://localhost:8080/shapetrees/TR/primer/ | grep -i location
```

Note that `http://localhost:8080/shapetrees` (no trailing slash) is answered by
Apache's own `DirectorySlash` redirect before these rules see it, so test the
namespace URI with the slash.
