<!--
SPDX-FileCopyrightText: 2026 contributors
SPDX-License-Identifier: GPL-2.0-only
-->

# hardware-specs-gpl

Hardware specs derived from GPL-2.0 source code, mostly the Linux kernel. Each spec here
is a derivative of the GPL code it cites, anchored to lines of that code at a pinned commit, and
is licensed GPL-2.0-only like it. Use them as a reference for Linux work, or if your project's
license does not matter to you. For specs you can use under other terms, see
[hardware-specs-docs](https://github.com/curtisgalloway/hardware-specs-docs) (datasheets only,
CC-BY-4.0) and
[hardware-specs-permissive](https://github.com/curtisgalloway/hardware-specs-permissive) (BSD, ISC, 0BSD, MIT
and Apache sources, Apache-2.0). A spec here may be an *overlay* that adds facts to a spec in
hardware-specs-docs, such as the device-tree facts of a chip whose device trees are all
GPL-2.0-only; CI checks this repository together with the other two so such an overlay always
finds its target.

**Every fact is cited, and the checker runs in CI.** Each spec here is a YAML file in spec
format 2: every fact is a record whose `support` names the evidence it rests on, a listed
document with a page or section, or lines of a source tree at a pinned commit, and every spec
has a verification record holding each fact's verdict. Every push and pull request runs
driver-lab's `spec.py` over the whole repository: a malformed record, a citation that does not
resolve, a source whose license this repository does not accept, or a fact without a current
verdict fails the build.

**Terms.** A *spec* is a hardware description that driver authors, people or AI agents, read
instead of the original sources. A *fact* is one record in it: a claim with a stable id and its
*support*, the citations it rests on. A *repos entry* (under `resources.repos`) pins a source
tree: its URL, commit and the SPDX license of the cited files (SPDX is the standard
license-identifier language); an *anchor* cites lines of it. An *overlay* adds facts to a spec in
another file or repository. `specs/board-specs.yaml` is this repository's *root marker*: it
states the repository's license and its *accepts list*, the licenses a cited source may carry.
The *license gate* is the check that fails a spec citing a source outside that list. A
*verification record* (`specs/resources/<name>.verify.yaml`) holds a verdict per fact, with a
hash of what the verdict was based on, so a changed fact shows as stale. The *views* are
generated reading copies: a Markdown view and an HTML *viewer*. Full definitions: driver-lab's
[glossary](https://github.com/curtisgalloway/driver-lab/blob/main/GLOSSARY.md).

## The specs

The published site, https://curtisgalloway.github.io/hardware-specs-gpl/, is rebuilt from `main` on every merge and every week; its
[index](https://curtisgalloway.github.io/hardware-specs-gpl/) lists every page. Each view carries a banner naming the commits it was built
from. Nothing generated is committed here: read the views on the site, or download a pull
request's `spec-views` artifact to read the views of a proposed change.

| Spec | Published views |
|---|---|
| [`specs/bcm2711.spec.yaml`](specs/bcm2711.spec.yaml): overlay on `bcm2711` in hardware-specs-docs | [viewer](https://curtisgalloway.github.io/hardware-specs-gpl/spec-ccedfed086925f56e4873ce03abe2b8bf40a70a2319445feb8c900a4b68d4a74.html) · [Markdown](https://curtisgalloway.github.io/hardware-specs-gpl/spec-ccedfed086925f56e4873ce03abe2b8bf40a70a2319445feb8c900a4b68d4a74.md) |
| [`specs/rk3588.spec.yaml`](specs/rk3588.spec.yaml): overlay on `rk3588` in hardware-specs-docs | [viewer](https://curtisgalloway.github.io/hardware-specs-gpl/spec-bf5dc176814f79b13ec5bbaa7fac9869f248c6a9f54447671777cf25b24a6b60.html) · [Markdown](https://curtisgalloway.github.io/hardware-specs-gpl/spec-bf5dc176814f79b13ec5bbaa7fac9869f248c6a9f54447671777cf25b24a6b60.md) |
| [`specs/rock5t.spec.yaml`](specs/rock5t.spec.yaml): overlay on `rock5t` in hardware-specs-docs | [viewer](https://curtisgalloway.github.io/hardware-specs-gpl/spec-1cfa4c0b5840fcccf34f7cb5caf7ec32973732760053288b220868397b0b736d.html) · [Markdown](https://curtisgalloway.github.io/hardware-specs-gpl/spec-1cfa4c0b5840fcccf34f7cb5caf7ec32973732760053288b220868397b0b736d.md) |
| `bcm2711` merged: the base spec with every overlay (hardware-specs-docs, hardware-specs-permissive, hardware-specs-gpl) | [viewer](https://curtisgalloway.github.io/hardware-specs-gpl/merged-803d78c39072f8a55e4d56c6427a2509b8af441ec58928896693dde90e022604.html) · [Markdown](https://curtisgalloway.github.io/hardware-specs-gpl/merged-803d78c39072f8a55e4d56c6427a2509b8af441ec58928896693dde90e022604.md) |
| `rk3588` merged: the base spec with every overlay (hardware-specs-docs, hardware-specs-permissive, hardware-specs-gpl) | [viewer](https://curtisgalloway.github.io/hardware-specs-gpl/merged-73f573c2d6db595d2f747ae5c352c5aa16d7ccd1ff15d474c9739e145fa35802.html) · [Markdown](https://curtisgalloway.github.io/hardware-specs-gpl/merged-73f573c2d6db595d2f747ae5c352c5aa16d7ccd1ff15d474c9739e145fa35802.md) |
| `rock5t` merged: the base spec with every overlay (hardware-specs-docs, hardware-specs-permissive, hardware-specs-gpl) | [viewer](https://curtisgalloway.github.io/hardware-specs-gpl/merged-0d03e342a8656a943f03b11a5ff2b2fa0e4a4eb315ba7ec2ccbb67a590faa6a3.html) · [Markdown](https://curtisgalloway.github.io/hardware-specs-gpl/merged-0d03e342a8656a943f03b11a5ff2b2fa0e4a4eb315ba7ec2ccbb67a590faa6a3.md) |

## Which repo does my spec go in?

**Placement rule:** a spec lives in the most restrictive repository among the sources it anchors
to. A spec may reference repositories with less restrictive licenses, never ones with more
restrictive licenses.

| Repo | License | Anchors allowed | Holds |
|---|---|---|---|
| `hardware-specs-gpl` | GPL-2.0-only | `[src:]` into any GPL-2.0-only or GPL-2.0-or-later tree, plus `[doc:]`, plus anything the permissive repo accepts | Linux-derived specs: references for Linux work, or for anyone who doesn't care about license. Easiest to verify. |
| `hardware-specs-docs` | CC-BY-4.0 (specs); per-file Apache-2.0 SPDX headers on CI files | `[doc:]` only | Specs built only from public datasheets, TRMs and standards |
| `hardware-specs-permissive` | Apache-2.0, plus a NOTICE file for the BSD/ISC/MIT sources | `[src:]` into BSD, ISC, 0BSD, MIT or Apache trees (and `GPL-2.0 OR MIT` files), plus `[doc:]` | TF-A, rpi-tools, Zephyr, FreeBSD, dual-licensed device trees. First material: the bcm2711 overlay (facts 2, 3, 6 below) |

The table is the license-split design's ([LICENSE-SPLIT.md](https://github.com/curtisgalloway/driver-lab/blob/main/docs/LICENSE-SPLIT.md#the-repos)),
verbatim; its "facts 2, 3, 6 below" are three boot-stub facts from BSD-licensed Raspberry Pi
tools, listed in that design's audit of the deleted specs.

This repository accepts sources licensed `GPL-2.0-only`, `GPL-2.0-or-later`, `Apache-2.0`, `MIT`, `BSD-2-Clause`, `BSD-3-Clause`, `ISC`, `0BSD` (`accepts:` in [specs/board-specs.yaml](specs/board-specs.yaml)).

In spec format 2, the table's `[src:]` is a `src` or `DT` support entry whose anchors point
into a `resources.repos` entry, and `[doc:]` a document support entry naming a
`resources.documents` entry. A spec here may cite `src` and `DT` facts anchored to `resources.repos` entries under GPL-2.0-only or GPL-2.0-or-later, anything the permissive repository accepts, plus documents.

## What is here

- `specs/`: the spec root. `board-specs.yaml` is the root marker; each spec is `<name>.spec.yaml`, and its verification record is `resources/<name>.verify.yaml`.
- `LICENSE`: the license.
- `.github/workflows/checks.yml` and `scripts/checks.sh`: the checks below.
- `.github/workflows/publish.yml`: builds the published views below.

## How a spec is written and checked

The method lives in [driver-lab](https://github.com/curtisgalloway/driver-lab). The contract for specs, the root marker and
verification records is the
[`spec-format`](https://github.com/curtisgalloway/driver-lab/blob/main/skills/spec-format/SKILL.md) skill (its JSON Schemas define each
record's fields); [`spec-verifier`](https://github.com/curtisgalloway/driver-lab/tree/main/skills/spec-verifier) writes the
verification records. CI checks out driver-lab at one pinned commit, installs `spec.py`'s
dependencies from its hash-pinned `skills/spec-format/requirements.txt`, and runs, through
`scripts/checks.sh`:

1. `check`: `spec.py check specs --require-license --require-verified <mode>`. The root
   marker, every spec and record against the schemas, names and references, composition, the
   license gate (every repos entry, cited or not) and each fact's verdict. The other spec repositories' `specs/` (hardware-specs-docs, then hardware-specs-permissive, at their `main`) are read as context roots (`--context-root`) so that overlays and root-qualified fact references resolve: their own errors are warnings here and fail only in their own repository's checks. On pull
   requests the mode is `pr`: a fact with no verdict, a stale one, or one staled by a change in
   another repository it references fails, so nothing merges unverified. On `main` the mode is
   `main`: a fact staled only by another repository's change is a warning, so an upstream merge
   never turns this repository red; the next pull request here must re-verify it. Re-run
   `spec-verifier` after editing a spec. The self-test's synthetic fixtures are exempt.
2. `resolve`: `spec.py resolve` on every spec. Each repos entry an anchor cites is fetched over
   HTTPS at its pinned commit (when `RESOLVE_SRC=1`, which the workflow sets), and every anchor's
   path, line range and symbol, and each cited file's license line, are checked. A repository
   whose fetch exceeds 50 MB (`SRC_FETCH_LIMIT_MB`) or the fetch timeout is skipped and counted
   in the summary; any other failure (a commit, file or symbol that does not exist) fails the
   build.
3. `render`: `spec.py render --format md` and `--format html`, each file's own view and the merged views: a
   spec that cannot be shown safely fails the build.
4. `self-test`: proves the license gate with this repository's own root marker, on driver-lab's
   format 2 fixture specs copied into temporary roots: the run fails unless the specs that do not
   fit fail with the gate's message and those that fit pass. With `RESOLVE_SRC=1` it also proves
   that anchors really resolve: a real pinned repository is fetched, a good anchor must resolve
   and a bad one fail. The fixtures are never published here as specs.

`.github/workflows/publish.yml` builds both views of every spec and the merged views with driver-lab's
`skills/spec-format/ci/publish.py`: on pull requests it uploads them as the `spec-views`
artifact; on `main` and weekly it verifies every page against the sources again and deploys the
site to GitHub Pages.

To run the same checks locally:

```bash
git clone https://github.com/curtisgalloway/driver-lab ../driver-lab
git clone https://github.com/curtisgalloway/hardware-specs-docs ../hardware-specs-docs
git clone https://github.com/curtisgalloway/hardware-specs-permissive ../hardware-specs-permissive
python3 -m venv .venv-spec
.venv-spec/bin/pip install --require-hashes -r ../driver-lab/skills/spec-format/requirements.txt
CHECKS_PYTHON=.venv-spec/bin/python RESOLVE_SRC=1 scripts/checks.sh all ../driver-lab ../hardware-specs-docs/specs ../hardware-specs-permissive/specs
```

`scripts/checks.sh --mode main ...` applies the `main` policy instead of the default `pr`. The
script needs bash and a Python with exactly the pinned packages (the interpreter in
`CHECKS_PYTHON`, otherwise `python3`); without them every step exits 3 (`missing dependency`).
Exit codes: 0 passed, 1 a check failed, 2 usage error, 3 missing precondition.

Check out the driver-lab commit that `.github/workflows/checks.yml` pins for an identical run.

## License

The specs and every other file here are licensed GPL-2.0-only ([LICENSE](LICENSE)); each
file states it in an `SPDX-License-Identifier` line.
