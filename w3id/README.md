# w3id.org/shapetrees

[`.htaccess`](.htaccess) is the redirect configuration for the
`https://w3id.org/shapetrees` namespace. It is kept here so it is versioned
alongside the vocabulary it resolves, but w3id.org serves it from a separate
repository — a copy in this repo has no effect on its own.

## Installing it

1. Fork [perma-id/w3id.org](https://github.com/perma-id/w3id.org).
2. Copy this directory's `.htaccess` to `shapetrees/.htaccess` in that fork
   (create the `shapetrees` directory; it holds nothing else).
3. Open a pull request. w3id.org asks that the PR say who maintains the
   namespace and give a contact address; the editors listed in the top-level
   [README](../README.md) are the maintainers.

Whenever a rule here changes, the change has to be sent to `perma-id/w3id.org`
again — nothing syncs automatically.

## What it resolves

| Request | Redirects to |
| --- | --- |
| `https://w3id.org/shapetrees` with an RDF `Accept` header | `https://shapetrees.github.io/specification/shapetrees.ttl` |
| `https://w3id.org/shapetrees` from a browser | `https://shapetrees.github.io/shapetrees.org/` |
| `https://w3id.org/shapetrees/TR/specification/` | `https://shapetrees.github.io/specification/` |
| `https://w3id.org/shapetrees/TR/primer/` | `https://shapetrees.github.io/primer/` |
| anything else under `/shapetrees/` | the same path on `https://shapetrees.github.io/shapetrees.org/` |

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
curl -sI -H 'Accept: text/turtle' http://localhost:8080/shapetrees | grep -i location
curl -sI http://localhost:8080/shapetrees/TR/specification/ | grep -i location
curl -sI http://localhost:8080/shapetrees/TR/primer/ | grep -i location
```
