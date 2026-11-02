# Contributing to nomatron-nomad-pack

## Repository layout

```text
nomatron-nomad-pack/
├── packs/nomatron/          # The pack — 6 items only
│   ├── templates/
│   ├── variables.hcl
│   ├── metadata.hcl
│   ├── outputs.tpl
│   ├── README.md
│   └── CHANGELOG.md
├── docs/                    # Platform guides (repo only)
├── examples/                # Example *.vars.hcl.example files (repo only)
├── .ci/                     # CI render fixtures (repo only)
├── CONTRIBUTING.md
├── LICENSE
└── .github/
```

## Day-to-day development

1. Edit pack templates/variables in [`packs/nomatron/`](packs/nomatron/).
2. Edit platform guides in [`docs/`](docs/) and example vars in [`examples/`](examples/).
3. Validate locally:

```bash
cd packs/nomatron
nomad-pack render --var-file=../../examples/production.byodb.vars.hcl.example . > /dev/null
nomad-pack plan  --var-file=../../examples/production.byodb.vars.hcl.example .
```

Do **not** run `nomad-pack fmt` on this pack. It rewrites Consul Template `{{` / `$tags` inside Nomad `template` blocks and produces jobs that fail Nomatron HCL parse (`Unsupported operator` on `| toJSON`).

4. Bump `pack.version` in [`packs/nomatron/metadata.hcl`](packs/nomatron/metadata.hcl) and update [`packs/nomatron/CHANGELOG.md`](packs/nomatron/CHANGELOG.md).
5. Open a PR.

When editing [`packs/nomatron/README.md`](packs/nomatron/README.md), keep Nomatron-specific content only; put nomad-pack install/usage in the [root README](README.md). Link to `docs/` with absolute GitHub URLs so links still work when the pack is fetched through `nomad-pack registry add`.
