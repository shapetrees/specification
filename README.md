# Shape Trees Specification

This repository contains the specification and supporting documentation
for [Shape Trees](https://w3id.org/shapetrees).

Shape trees marry RDF vocabularies, shapes, and resources into "little trees"
that provide machine to machine interoperability, combining them into concepts
that humans can easily comprehend, such as medical records, notes, notebooks,
calendars, and financial records.

For applications that operate on more complex and interconnected resources,
Shape Trees express the layout of those resources and associate them with
their respective shapes.

* Specification Editor's Draft - [Rendered](https://w3id.org/shapetrees/TR/specification/) - [Source](index.bs)
* Primer Editor's Draft - [Rendered](https://w3id.org/shapetrees/TR/primer/) - [Source](https://github.com/shapetrees/primer/)
* Specification Test Suite - [Source](https://github.com/shapetrees/test-suite)

Shape Trees are a
[W3C Solid Community Group](https://www.w3.org/community/solid/) work effort.

Changes to the Shape Trees specification and supporting documentation are
reviewed by the editors:

- [Eric Prud'hommeaux](https://github.com/ericprud)
- [Justin Bingham](https://github.com/justinwb)

## Namespace

The Shape Trees vocabulary namespace is `https://w3id.org/shapetrees#`, and
is defined by [shapetrees.ttl](shapetrees.ttl). Prior drafts used
`http://www.w3.org/ns/shapetrees#`; implementations should treat that as a
deprecated alias for the same terms.

| URL | Content |
| --- | --- |
| <https://w3id.org/shapetrees> | The [vocabulary](shapetrees.ttl) (Turtle) |
| <https://w3id.org/shapetrees/TR/specification/> | This specification |
| <https://w3id.org/shapetrees/TR/primer/> | The [primer](https://github.com/shapetrees/primer/) |

The `w3id.org` entries redirect to GitHub Pages, where the documents are
actually hosted:

| Repository | GitHub Pages |
| --- | --- |
| [shapetrees/shapetrees.org](https://github.com/shapetrees/shapetrees.org) | <https://shapetrees.github.io/shapetrees.org/> |
| [shapetrees/specification](https://github.com/shapetrees/specification) | <https://shapetrees.github.io/specification/> |
| [shapetrees/primer](https://github.com/shapetrees/primer) | <https://shapetrees.github.io/primer/> |

The redirect rules live in [`w3id/.htaccess`](w3id/.htaccess); see that
directory's [README](w3id/README.md) for how to submit them to
[perma-id/w3id.org](https://github.com/perma-id/w3id.org).

These documents were previously published at `shapetrees.org`, which is no
longer hosted.

## Building

The specification is written in [Bikeshed](https://speced.github.io/bikeshed/).
To render it locally:

```bash
python3 -m pip install bikeshed && bikeshed update
bikeshed spec index.bs
```

Every push to `main` rebuilds the spec and publishes it to GitHub Pages via
[`.github/workflows/publish.yml`](.github/workflows/publish.yml).

## Contributing

Use the standard fork, branch, and pull request workflow to propose changes
to the specification. Please make branch names informative (e.g. by including
the issue or bug number).

Editorial changes that improve the readability of the spec or correct
spelling or grammatical mistakes are welcome.

Please read [CONTRIBUTING](CONTRIBUTING.md) about licensing contributions.

## Code of Conduct

All documentation, code and communication under this repository are
covered by the
[W3C Code of Ethics and Professional Conduct](https://www.w3.org/Consortium/cepc/).
