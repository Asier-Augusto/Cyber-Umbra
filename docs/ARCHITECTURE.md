# Architecture (conceptual)

> Beta preview. This describes the *design and methodology* of Cyber Umbra at a high level.
> It is not the implementation, and the production engine is not included in this
> repository.

Cyber Umbra is organized as a pipeline from **public knowledge** to **reviewed,
authorized assessment**. Each stage hands a well-defined artifact to the next, and the
consequential stages are gated by a human.

## Stages

1. **Ingestion** — open security corpora (weakness taxonomies, attack patterns, public
   advisories) are parsed into normalized records with provenance. Sources are pinned and
   verified; ingested content is treated as **untrusted data**, never as instructions to
   the system.

2. **Knowledge store** — a relational store (PostgreSQL) is the source of truth for
   ingested knowledge: what was learned, from where, and with what confidence.

3. **Graph projection** — the knowledge is projected into a graph (Neo4j) so that
   relationships (technique ↔ weakness ↔ observable signal) can be traversed and reasoned
   over. The graph is a **reconstructible projection** of the store, not a second source
   of truth.

4. **Observation** — for an authorized target, the web surface is mapped through standard,
   well-behaved tooling (a real browser driven through an intercepting proxy). The result
   is a **surface inventory** with evidence, correlated against proxy history.

5. **Reasoning** — observed surface is matched against projected knowledge to produce
   **candidate** findings and paths. A match is a lead for a human, never a conclusion.

6. **Human review & optional active validation** — candidates are reported to a human.
   Any step that goes beyond passive analysis is **bounded, authorized, and confined** to
   the agreed scope.

7. **Reporting** — confirmed and candidate findings are assembled into an assessment
   report for the authorized engagement.

## An epistemic lifecycle

Rather than flipping between "unknown" and "vulnerable," findings move through explicit
states, and the jump to *confirmed* is reserved for human-validated evidence:

```
OBSERVED → KNOWN → INFERRED → PROPOSED → SUPPORTED → CONFIRMED / REJECTED
```

Machine learning may raise or lower confidence and suggest relationships, but it never
promotes a finding to **CONFIRMED** on its own.

## Two data stores, one truth

- **PostgreSQL** holds the knowledge of record.
- **Neo4j** is a projection built from it for relationship reasoning, and can be rebuilt
  from the store at any time.

## Design principles

- **Safety is enforced in code, not asserted in prose.**
- **Analysis before action**; passive before active; anonymous before authenticated.
- **Candidate ≠ confirmed.**
- **Provenance everywhere** — every piece of knowledge knows where it came from.

See [`GOVERNANCE.md`](GOVERNANCE.md) for the authorization model.
