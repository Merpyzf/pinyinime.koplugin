# Third-party notices

## Rime pinyin-simp abbreviation data

The file `data/pinyin_abbr_data.lua`, and the base candidates retained in the
merged abbreviation table of `data/phrase_overlay.lua`, contain initials-based
Simplified Chinese pinyin phrase data generated from
[`rime/rime-pinyin-simp`](https://github.com/rime/rime-pinyin-simp).

- Upstream license: Apache License 2.0
- Imported through: `koreader/koreader` pull request #15610
- Pinned KOReader commit: `66ef609fbc5eab059ee07930a71f4300f8d37065`
- Vendored file SHA-256:
  `234e5a2cd582a161a48494068ec9e57171193763782efcd0f0b21977e8817dc9`
- Local change: the data remains unchanged; the input engine reads at most the
  first 10 candidates for each abbreviation.

The complete upstream license is included in `LICENSE.rime-pinyin-simp`.

## Apple layouts and Rime double-pinyin cross-check

The generated files `data/shuangpin_sogou_microsoft.lua`,
`data/shuangpin_pinyin_jiajia.lua`, `data/shuangpin_flypy.lua`, and
`data/shuangpin_common.lua` implement the key layouts and zero-initial rules
documented by Apple. The Apple 常用 layout is exposed as 自然码双拼 because it
matches the pinned 自然码 rules in
[`rime/rime-double-pinyin`](https://github.com/rime/rime-double-pinyin).
The other Rime schemes are used as a cross-check, and the 小鹤 map also retains
compatible alternate zero-initial codes from `double_pinyin_flypy.schema.yaml`.

- Apple layout documentation:
  https://support.apple.com/zh-cn/guide/chinese-input-method/cimc29a772a9/mac
- Apple input rules:
  https://support.apple.com/zh-cn/guide/chinese-input-method/cimf64446397/mac

- Upstream license: GNU General Public License 3.0
- Pinned upstream commit: `01a13287cbd27819be1c34fa1ddc1b3643d5001b`
- Generated file SHA-256 values:
  - 搜狗双拼 / 微软双拼: `b95381c873f31054ddb8bac7137ab4319761393a55a4f34afe4bde03cbd7b4b0`
  - 拼音加加双拼: `73fdc00c6b80f3c3ae34e800e4b103188d6237ba3d2dbb2132be57c4d926eefb`
  - 小鹤双拼: `14b0cc17fb676976ec1bdb7d6693c9762b0fb632ea24b780033f4c603bfbe11b`
  - 自然码双拼: `54aebd2cd68bb09b47f60f296a9e1eb7aab19110a80d36384fdabb9f10d4de45`
- Local change: the layouts are applied at build time to the plugin's shared
  pinyin syllable inventory. Runtime decoding uses the generated two-key
  lookup tables; `m`, `n`, `ng`, and `hng` are handled by the plugin's explicit
  apostrophe escape syntax.

The complete upstream license is included in `LICENSE.rime-double-pinyin`.

## Rime Ice, Jieba, and Wanxiang phrase overlay

`data/phrase_overlay.lua` contains a bounded exact-phrase overlay generated
from Rime Ice's annotated Simplified Chinese dictionaries, the Jieba
general-purpose frequency dictionary, Wanxiang's modern input-method weights,
and the plugin's explicit reading, device, input-method, and technology
allowlist. Its abbreviation table merges those additions with the Apache-2.0
pinyin-simp data documented above.

- Rime Ice source: [`iDvel/rime-ice`](https://github.com/iDvel/rime-ice)
- Rime Ice license: GNU General Public License 3.0
- Pinned Rime Ice commit: `3a543652a42c21904c62bd881d65e987600f0722`
- Rime `base.dict.yaml` SHA-256:
  `dfdf4b553bbc70bb4809da6b9f90aa4abce752ed211d94af37df2350e0e7394f`
- Rime `ext.dict.yaml` SHA-256:
  `f715e0cafdd02964241d10ac970f5985c9c78c4281e7d323f1d98a324adad614`
- Jieba source: [`fxsjy/jieba`](https://github.com/fxsjy/jieba)
- Jieba license: MIT
- Pinned Jieba commit: `67fa2e36e72f69d9134b8a1037b83fbb070b9775`
- Jieba `dict.txt` SHA-256:
  `7197c3211ddd98962b036cdf40324d1ea2bfaa12bd028e68faa70111a88e12a8`
- Wanxiang source: [`amzxyz/rime-wanxiang`](https://github.com/amzxyz/rime-wanxiang)
- Wanxiang license: Creative Commons Attribution 4.0 International
- Pinned Wanxiang commit: `6c792a2e68c8382f9c63e8bed74c5cf247f1b1a9`
- Wanxiang `dicts/jichu.dict.yaml` SHA-256:
  `35437365ecef172dbbe4238062dccd69eb4af1989ee30b21d98fb515dae4a6ad`
- Generated overlay SHA-256:
  `710cbbfc963c1765326540039718cb35cb491e9c2949f4323d8ef33bcb0ffe9b`

The automatic selection contains only 2–4 character Han phrases. The first
7,000 accepted automatic entries retain the existing Jieba/Rime ordering; the
remaining bounded tail uses reciprocal-rank fusion over Jieba, Rime, and
reading-matched Wanxiang ranks. Wanxiang pinyin is stripped of tone marks and
must exactly match the Rime-selected reading, so polyphonic readings are never
merged by word alone. The generated output is further bounded and
de-duplicated by code; it does not contain any complete upstream dictionary.
Source revisions, hashes, filters, source ranks, and coverage results are recorded in
`tools/phrase_overlay_report.json`, and the preferred form for modification is
the pinned source dictionaries together with `tools/generate_phrase_overlay.py`
and `tools/phrase_allowlist.tsv`.

The Rime Ice notice is in `LICENSE.rime-ice`; the complete GPL-3.0 text already
shipped by this plugin is `LICENSE.rime-double-pinyin`. The complete Jieba MIT
license is included in `LICENSE.jieba`.
The complete Wanxiang CC-BY-4.0 license is included in `LICENSE.wanxiang`.

## Academic and general vocabulary supplement

`data/academic_supplement.sqlite3` is a separate, read-only fallback database
for ordinary and academic terms. The runtime queries it only when the
byte-identical main `phrase` result contains fewer rows than the requested
candidate limit. The generated artifact contains 560,885 rows, is 29,491,200
bytes, and has SHA-256
`6fa88bd7054021a28baa4ce1bc8f716a97499f840139e7987bb4ad0eb0fa953b`.
The unchanged parent `data/wanxiang.sqlite3` has SHA-256
`f96f3e687793366a2a601acb174563cf2aed0a1c4bcdd0fe1152d0f544374638`.

The preferred forms for modification are `tools/academic_lexicon.tsv`
(SHA-256
`10117b2a581b61973029cd75576188b7ecc2171455de0703855e830ba37dd138`),
`tools/general_coverage_lexicon.tsv` (SHA-256
`aa936b2eb4ca302a11f64203320b080c0f5ae66568f4f136ba18bc5c3a6042cc`),
their JSON manifests, and the corresponding build tools. Validation-only
wordfreq and Universal Dependencies rows are not used to select or rank this
released supplement.

The supplement combines and modifies the following licensed sources:

- [THUOCL](https://github.com/thunlp/THUOCL), commit
  `a30ce79d895d01ab5132a5c74c29703ff7efb4cc`, MIT License, Copyright
  (c) 2018 THUNLP. The IT, finance, law, medical, animal, car, and food lists
  provide frequency-bearing domain evidence. The complete notice is included
  in `LICENSE.thuocl`.
- [Rime Frost](https://github.com/gaboolic/rime-frost), commit
  `69cbcf8937ae03c03792fa285dca7f79f80715bc`, GNU GPL 3.0. The computer,
  mathematics/physics/chemistry, medicine, geography, history, literature,
  sport, animal, and industrial-product dictionaries provide annotated pinyin
  and domain evidence. The complete license is included in
  `LICENSE.rime-frost`.
- [Rime Ice](https://github.com/iDvel/rime-ice), commit
  `3a543652a42c21904c62bd881d65e987600f0722`, GNU GPL 3.0, and
  [Jieba](https://github.com/fxsjy/jieba), commit
  `67fa2e36e72f69d9134b8a1037b83fbb070b9775`, MIT. Their notices and
  complete licenses are already documented above in `LICENSE.rime-ice`,
  `LICENSE.rime-frost`/`LICENSE`, and `LICENSE.jieba`.
- [CC-CEDICT](https://www.mdbg.net/chinese/dictionary?page=cc-cedict),
  downloaded source SHA-256
  `725a09738b42ab01d6ff4f95456cd1b3ed91a9df7a923e88b7c16a05077b3970`,
  Creative Commons Attribution-ShareAlike 4.0. It supplies licensed lexical
  entries and reading evidence.
- Chinese Wikipedia contributors, Creative Commons
  Attribution-ShareAlike 4.0. The academic classification was derived from
  pinned `page`, `categorylinks`, and `linktarget` dump files with SHA-256
  values recorded in `tools/academic_lexicon_manifest.json`; the generated
  category index has SHA-256
  `190738e80ec9565a37a5f5ebeffa15239daae0a2259d6099284f568e2e1acb0a`.
  Named-concept readings also use the pinned
  [fcitx5-pinyin-zhwiki](https://github.com/felixonmars/fcitx5-pinyin-zhwiki)
  `0.3.0/zhwiki-20260416.dict.yaml` release, SHA-256
  `5c140e462f9c00a119500b7fec0d3b927f0f83920001a7ea408e26748d09ea07`;
  its generator code is Unlicense and its Wikipedia-derived content remains
  CC-BY-SA-4.0.

The local build converts terms to Simplified Chinese, retains only 2–10 Han
characters (2–6 for the bounded Wikipedia named-concept tail), assigns the
Ministry of Education's 14-category/117-discipline taxonomy, filters invalid
readings, merges duplicate `(pinyin, text)` pairs, caps ranks at 500, and
stores only baseline-missing pairs. These are modifications; downstream
redistributors must preserve attribution, indicate modifications, provide the
license, and comply with ShareAlike for the CC-BY-SA-covered material. The
complete CC-BY-SA-4.0 legal code is included in
`LICENSE.cc-by-sa-4.0`.

## Locally authored CC0 prediction material

`tools/ai_prediction_seed.tsv` is the project's deterministic, AI-assisted,
manually reviewed prediction seed. It was authored independently of the
licensed corpora described below and is not a relicensing of DuReader or
Wanxiang text.

- Declared source: `original-ai-authored`
- License dedication: CC0-1.0, to the extent the project owns copyright or
  related rights in the material
- Generated seed SHA-256:
  `8e0879fb1fe20253133bb3f04287c72643f749e2a43a621de4f80f6217c25848`
- Seed manifest SHA-256:
  `12a1e3ef649be5bb2a9010df2dc33d6b43ccbcf13a1d189ed5e59d1e0a0ffa1c`
- Generator SHA-256:
  `b4ea711a5400735eabb0400d45f48c4ab8b07fd12d7e58da52a540e5323cf8ad`
- Size and scope: 257,472 bytes; 1,152 contexts; 4,577 relations

The preferred form for modification is
`tools/generate_ai_prediction_seed.py`; running it with `--check` verifies the
committed TSV and manifest byte-for-byte. The generator and manifest state
that validation and release-blind answers were not used to author, select, or
rank these associations. The separate development corpus is likewise declared
CC0-1.0 in `tools/prediction_corpus_manifest.json`; its development artifact
SHA-256 is
`ef82aa5e9f4679a22a662dd9d61715873c84dd1ad6618c7cf3eb2ed1caa05d98`.
Redistributors should preserve these manifests so that locally dedicated CC0
material remains distinguishable from the licensed corpus seed.

## Licensed next-text corpus distillation

`tools/corpus_prediction_seed.tsv.gz` is a modified, compressed statistical
artifact built from one licensed Chinese corpus. The raw corpus is a build
input and is not included in the plugin, but its license and attribution
requirements continue to apply to the generated seed and to prediction rows
copied from it into `data/wanxiang.sqlite3`. The artifact is not CC0.

The build tool has a tested Tatoeba parser, but the committed source manifest,
seed, and database contain no Tatoeba-derived relation. Tatoeba sentences were
excluded because the compact format does not retain the sentence ID and
individual contributor mapping required for reliable CC-BY attribution. A
future release must not add that source without preserving compliant
sentence-level provenance and attribution.

### Baidu DuReader-Robust

- Source: [`baidu/DuReader`, `DuReader-Robust`](https://github.com/baidu/DuReader/tree/c625076b06da8f56d59f19c41c73bd580a98a347/DuReader-Robust)
- Pinned commit: `c625076b06da8f56d59f19c41c73bd580a98a347`
- `train.json` SHA-256:
  `137e65191e2f0895d0b3ae8a2af2387b2aa2342642476a616287e150740016ce`
- `dev.json` SHA-256:
  `eda029d96334a413a5b58d003b318cb84a8a81ce09280de7f9ea82b1c4999006`
- Copyright notice: Copyright 2020 Baidu.com, Inc. All Rights Reserved
- License: Apache License 2.0
- Local modification: questions and answer spans were normalized, segmented,
  aggregated with support thresholds, filtered, ranked, and emitted only as
  bounded context/continuation relations.

The pinned `DuReader-Robust` tree contains the copyright and Apache-2.0 notice
in its README and no separate upstream `NOTICE` file. The complete canonical
Apache License 2.0 text already shipped in this plugin is
`LICENSE.rime-pinyin-simp`; it also supplies the required license text for this
DuReader-derived component. Redistributors must preserve the Baidu copyright
notice above and mark the generated seed as modified.

### Generated licensed artifact

- Source manifest: `tools/prediction_sources.json`, SHA-256
  `71c97b11e91aee41594851d817c7f0e98f737e8521b8c231dc98b5e719972faf`
- Generator: `tools/build_prediction_lexicon.py`, SHA-256
  `a1695c24db956b1fec02aa032f2d44ed78ec5030a015da8907b6c4322831405b`
- Wanxiang `jichu` segmentation input SHA-256:
  `35437365ecef172dbbe4238062dccd69eb4af1989ee30b21d98fb515dae4a6ad`
- Wanxiang Simplified/Traditional map SHA-256:
  `f73b5160a003aa774fc648adb738456e9eb35380e5e1b0cf5b49a9b901eb4fe0`
- Generated seed: `tools/corpus_prediction_seed.tsv.gz`, SHA-256
  `6f4a93085d8b41dd803ea78e3e3bba81daa4e732ce0d77b2682841aa9ee17f5a`
- Generated manifest: `tools/corpus_prediction_seed_manifest.json`, SHA-256
  `f71cd76840c798174b6702c73962388baf10eacd0872d8033bdf1e524c0ab8de`
- Generated size: 26,654 bytes; 1,684 contexts; 2,771 relations

Individual generated rows record aggregate support and source counts, not
per-document provenance. The seed and the database component derived from it
carry the Apache-2.0 DuReader notice above.
`tools/corpus_prediction_report.json` records filters, thresholds, input
statistics, and samples; it is a build report, not a substitute for required
attribution.

### Schema-v4/v5 candidate artifacts

Two additional aggregate-only DuReader artifacts support the release-gated
schema-v4 B/C experiment and its schema-v5 packed/transition successor. They
carry the same Apache-2.0 Baidu notice above.
They are shipped as reproducible build inputs, but the current schema-v3
`data/wanxiang.sqlite3` does not contain their rows.

- Composition generator: `tools/build_composition_lexicon.py`, SHA-256
  `c0357c9b99df9ebaac5b382bdb662f790ba557bda30d95241474dd67b7063390`
- Composition seed: `tools/corpus_composition_seed.tsv.gz`, 10,387 bytes,
  942 contexts and 1,673 relations, SHA-256
  `0576f7fddc60a697675ece207a394bc3ae387928f6338abb94c0fcfd9d34e8d2`
- Composition manifest SHA-256:
  `cd42d250e854e3db00c01b6fee0837440d7e757c8efadba45c1ac508b4697249`
- Missing-phrase generator: `tools/build_missing_phrase_lexicon.py`, SHA-256
  `72038e3651f9170ad24ac7f4d5ad33d347adceb717499fe5dd9219f6b234174a`
- Missing-phrase seed: `tools/corpus_missing_phrase_seed.tsv.gz`, 6,887 bytes,
  1,121 evidence rows, SHA-256
  `7f820655fe716c50b61adc39e975268c288e29f97b55cbcc2a9304f9e47f02d3`
- Missing-phrase manifest SHA-256:
  `86ea5a2572bd1bd402d820d3bf883a8150834de02da479c2a37d9d1591ad11d0`

Both generators verify the source manifest, raw input hashes, Wanxiang
segmentation and Simplified/Traditional-map hashes. Tuning, validation, and
release-blind paths are rejected. Only document support, occurrence counts,
quality scores, and bounded Han relations are emitted; raw questions, answers,
document identifiers, and webpage contexts are absent.

## Wanxiang full SQLite lexicon

`data/wanxiang.sqlite3` is a build-time normalized form of the Han-only entries
imported by Wanxiang's complete `wanxiang.dict.yaml` manifest. It is a
standalone, read-only database shipped and opened by this plugin; it does not
contain or access any KOReader database. “Plugin-owned” in runtime
documentation refers to file location and lifecycle, not copyright ownership
of third-party components.

- Source: [`amzxyz/rime-wanxiang`](https://github.com/amzxyz/rime-wanxiang)
- Upstream license: Creative Commons Attribution 4.0 International
- Attribution: Rime Wanxiang by `amzxyz` and upstream contributors
- Pinned upstream commit: `6c792a2e68c8382f9c63e8bed74c5cf247f1b1a9`
- Schema-v1 generated database SHA-256 (before next-text prediction):
  `5a82ad420e5f21193bc94da88e3481bfd465668007a11de13796cf27f1c980b3`
- Released augmented database SHA-256:
  `05b51c39ce855019614ffb6be06bf788e211b5fb36bfbd9fa1539696b07758b4`
- Released augmented database size: 100,651,008 bytes
- Prediction table: schema v3, 80,000 contexts, 182,148 rows, at most five
  candidates per context
- Builder: `tools/build_wanxiang_db.py` version 5.0.0, SHA-256
  `4f9d332ba2972f83dc718886d644824bd2a2eafab697ce004445d96c2d0f94a8`
- Build report: `tools/wanxiang_db_report.json`, SHA-256
  `130f33454951b4ca46bb13f0823e59394aa22de015b8607228b435acc95573f2`
- Local changes: tone marks are removed, umlaut-u is represented as `v`, syllable
  boundaries are retained with apostrophes, unsupported or common
  Traditional-only forms are filtered, duplicate `(pinyin, text)` entries are
  merged, source priors are recorded, and the existing bounded phrase overlay is
  merged as a compatibility source. Schema v3 also contains a bounded next-text
  table. Its highest-priority relations are development-only counts from this
  project's original phrase-boundary corpus, followed by an independently
  authored CC0 seed, the licensed DuReader corpus seed documented
  above, high-confidence Wanxiang `jichu` phrases, and lower-priority
  `lianxiang` splits. A separate five-row phrase layer mined from the original
  long-sentence tuning corpus is marked with its own source bit and penalty.
  These local layers add no network, model, or runtime dependency.

The database is a collective generated artifact. Its phrase and prediction
components include CC-BY-4.0 Wanxiang data, GPL-3.0 Rime Ice overlay data, MIT
Jieba overlay data, Apache-2.0 pinyin-simp and DuReader-derived data,
and locally authored CC0 prediction data. No Tatoeba-derived relation is
present in this release.
The database metadata field `license_id=CC-BY-4.0` describes the Wanxiang
lexical base only; it is not a license declaration for the entire combined
database. Redistributors must ship this notice and every applicable license
identified above, preserve attribution, and must not relicense the complete
database as CC0 or solely CC-BY-4.0.

Every imported source hash, filter count, rank sample, database size, and schema
version is recorded in `tools/wanxiang_db_report.json`. The reproducible build
inputs include `tools/wanxiang_sources.json`, `tools/ai_prediction_seed.tsv`,
`tools/ai_prediction_seed_manifest.json`,
`tools/corpus_prediction_seed.tsv.gz`,
`tools/corpus_prediction_seed_manifest.json`,
`tools/prediction_corpus_development.tsv`, and
`tools/build_wanxiang_db.py`. Evaluation reports are separate from build
inputs and are valid release evidence only when their database SHA-256 matches
the database hash above. The complete upstream Wanxiang license is included in
`LICENSE.wanxiang`.
