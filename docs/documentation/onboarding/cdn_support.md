# CDN Support

To support a multi-cdn strategy, multiple CDNs are an obvious need. What is not always
obvious, is how feature sets overlap and, sometimes, collide. Airspace's aim is to
streamline product overlap, while enabling power users to be more specific where
allowed,  with Airspace being the validation and sanity check guardrail for your
configuration.

Airspace supports the following CDNs:

- Akamai
- Cloudfront
- Edgecast
- Fastly

> Fastly is required to be in the mix. All CDN configs are shielded by Fastly.

## CDN Support Matrix

| CDN        | Change Propagation Time | Custom Domains | Feature Y | Feature Z |
|------------|-------------------------|----------------|-----------|-----------|
| Fastly     | 2m  to 5m               | ✅              | ❌         | ✅         |
| Edgecast   | 30m to 2h               | ✅              | ❌         | ✅         |
| Cloudfront | 10m to 30m              | ❌              | ❌         | ✅         |
| Akamai     | 1h to 2h                | ✅              | ❌         | ✅         |

## Constraints

TBD.
