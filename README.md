# plugin-resource

The `resource` plugin kind for OpenCharly — decode of the authored `resource:`
entity.

`plugin-resource` is a **kind provider** that dispatches via the
`pb Invoke(OpLoad)` envelope: it decodes the authored `resource:` node into its
core spec type and re-marshals it as canonical JSON. It serves itself in **both**
placements (compiled-in or out-of-process) — kinds are pb-shape, so no kit
contract is needed.

## What it provides

| Capability | Surface |
|---|---|
| `kind:resource` | decode of the authored `resource:` entity (the `resource:` kind) |

## How to use it

Compose the plugin candy where a box or deploy authors a `resource:` node:

```yaml
- '@github.com/opencharly/plugin-resource/candy/plugin-resource:<tag>'
```

## Layout

- `candy/plugin-resource/` — the plugin module: `plugin.go` (the kind provider +
  `NewMeta()`), `resolve.go` (the entity decode), `schema/resource.cue`,
  `params/cue_types_gen.go`, `cmd/serve/main.go`.
- `charly.yml` — the root project manifest (`discover: candy`).
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.

## Related

- Owning skill: `/charly-internals:plugin` — the plugin/provider model and the
  kind-decode seam this provider implements. This candy carries no `skill:`
  entity of its own; the gap is tracked in
  [opencharly/opencharly#291](https://github.com/opencharly/opencharly/issues/291).
- `/charly-image:layer` — the candy authoring surface.
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI.
