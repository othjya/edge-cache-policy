# edge-cache-policy

Personal edge/CDN hostname policy.

This repository keeps a small supplemental hostname list for selected high-volume asset and CDN endpoints. It is intentionally conservative and only tracks endpoints that are useful to keep separate from regular interactive traffic.

## Raw List

```text
https://raw.githubusercontent.com/othjya/edge-cache-policy/main/rules/assets.list
```

## Layout

- `rules/assets.list`: curated hostname rules.
- `assets/edge.svg`: neutral edge/CDN policy icon source.
- `assets/edge.png`: PNG icon for clients that do not render SVG icons.
- `assets/server.svg`: neutral server policy icon source.
- `assets/server.png`: PNG server icon for clients that do not render SVG icons.
- `snippets/provider.yaml`: local integration snippet.
- `.github/workflows/validate.yml`: basic syntax validation.

## Maintenance

- Prefer exact `DOMAIN` or scoped `DOMAIN-SUFFIX` entries.
- Do not add broad keyword rules such as `DOMAIN-KEYWORD,download` or `DOMAIN-KEYWORD,update`.
- Keep login, API, store, community, and account domains out of this list unless they are known to carry large downloads.
- Do not duplicate domains that are already covered by broader upstream lists.

## Notes

Routing by byte count is not supported by static hostname policies, so this list classifies selected high-volume traffic by domain and CDN hostname.
