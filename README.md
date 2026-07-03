# Ultrahuman (ultrahuman)

Ultrahuman makes the Ring AIR and Ring Pro smart rings and the M1 continuous glucose monitor (CGM) - a subscription-free metabolic-health wearable ecosystem. Its Partner (UltraSignal) API lets approved partners read user-consented health metrics - sleep, HRV, resting heart rate, skin temperature, SpO2, movement/recovery indexes, VO2 max, and (with the M1 patch) continuous glucose - over an OAuth 2.0-secured REST API. A separate UltraSignal developer program offers raw sensor streams (PPG, temperature, accelerometer) from the Ring AIR via a loaned developer kit.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/ultrahuman/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/ultrahuman/refs/heads/main/apis.yml)

## Access Model

Ultrahuman's API is **real and documented, but not self-serve**:

- **Partner (UltraSignal) API** - OAuth 2.0 (Authorization Code Grant + Refresh Token flow) at base `https://partner.ultrahuman.com`, with the scopes `profile`, `ring_data`, and `cgm_data`. Partners **apply** to the developer program and are issued a Client ID, Client Secret, and a registered redirect URI during onboarding (applications for legitimate health/wellness use cases process on the order of one to two weeks). End users authorize data sharing from the Ultrahuman app (Profile → Settings → Partner ID). Access tokens live ~1 day (86400s) and refresh tokens rotate on each exchange.
- **Personal token** - an individual can read their own ring data with a personal Bearer token via `GET /api/v1/partner/daily_metrics`.
- **UltraSignal developer kit** - a separate, application-gated program granting raw Ring AIR sensor streams (PPG, temperature, accelerometer) with a loaned developer kit.

The OpenAPI in this repo is flagged **`x-endpointsModeled: true`**: endpoint paths, OAuth flows, scopes, query parameters, and the documented metric families come from Ultrahuman's public partner developer docs, but exact request/response schemas are modeled approximations and should be verified against the live portal.

## Tags

- Wearables
- Smart Ring
- Health
- Metabolic Health
- Sleep
- HRV
- Recovery
- CGM
- Glucose
- Digital Health

## Timestamps

- **Created:** 2026-07-03
- **Modified:** 2026-07-03

## APIs

### Ultrahuman Metrics API

Reads user-consented Ring AIR / Ring Pro daily metrics via the `ring_data` scope - sleep stages, duration, efficiency and sleep score, HRV (rMSSD), resting and night heart rate, skin temperature deviation, SpO2, steps, movement index, recovery index/score, metabolic score, and VO2 max. `GET` by date (YYYY-MM-DD) or by a start/end epoch window (max 7 days).

- **Human URL:** [https://vision.ultrahuman.com/developer-docs](https://vision.ultrahuman.com/developer-docs)
- **Base URL:** `https://partner.ultrahuman.com`

#### Properties

- [Documentation](https://vision.ultrahuman.com/developer-docs)
- [API Reference](https://www.ultrahuman.com/blog/accessing-the-ultrahuman-partnership-api/)
- [OpenAPI](openapi/ultrahuman-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/ultrahuman.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)

### Ultrahuman CGM (Glucose) API

Reads continuous glucose data via the `cgm_data` scope, for users with an active Ultrahuman M1 CGM patch - individual readings (mg/dL, ~5-minute cadence), average glucose, glucose variability, estimated HbA1c, and time-in-target-range percentage. Surfaced through the same metrics endpoint, gated on the `cgm_data` scope.

- **Human URL:** [https://vision.ultrahuman.com/developer-docs](https://vision.ultrahuman.com/developer-docs)
- **Base URL:** `https://partner.ultrahuman.com`

#### Properties

- [Documentation](https://vision.ultrahuman.com/developer-docs)
- [OpenAPI](openapi/ultrahuman-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Ultrahuman User Info API

Reads the authorized user's basic profile via the `profile` scope - user ID, time zone, and similar account metadata used to correlate metric payloads to a partner-linked user.

- **Human URL:** [https://vision.ultrahuman.com/developer-docs?type=oauth](https://vision.ultrahuman.com/developer-docs?type=oauth)
- **Base URL:** `https://partner.ultrahuman.com`

#### Properties

- [Documentation](https://vision.ultrahuman.com/developer-docs?type=oauth)
- [OpenAPI](openapi/ultrahuman-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### Ultrahuman OAuth 2.0 API

OAuth 2.0 authorization for the Partner API - Authorization Code Grant plus Refresh Token flow across the `profile`, `ring_data`, and `cgm_data` scopes. Includes authorize, token, and revoke endpoints. Client ID/secret and a registered redirect URI are issued during partner onboarding.

- **Human URL:** [https://vision.ultrahuman.com/developer-docs?type=oauth](https://vision.ultrahuman.com/developer-docs?type=oauth)
- **Base URL:** `https://partner.ultrahuman.com`

#### Properties

- [Documentation](https://vision.ultrahuman.com/developer-docs?type=oauth)
- [API Reference](https://www.ultrahuman.com/blog/accessing-the-ultrahuman-partnership-api/)
- [OpenAPI](openapi/ultrahuman-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)

### UltraSignal Sensor Platform API

UltraSignal is Ultrahuman's wearable developer platform for building custom algorithms on raw Ring AIR sensor streams - photoplethysmography (PPG), temperature, and accelerometer data. Access is application-gated with a loaned developer kit. No public endpoint contract is documented, so this API is listed for discovery without modeled endpoints.

- **Human URL:** [https://www.ultrahuman.com/ultrasignal/](https://www.ultrahuman.com/ultrasignal/)
- **Base URL:** `https://partner.ultrahuman.com`

#### Properties

- [Documentation](https://www.ultrahuman.com/ultrasignal/)

## Common Properties

- [Website](https://www.ultrahuman.com)
- [LinkedIn](https://www.linkedin.com/company/ultrahuman)
- [Documentation](https://vision.ultrahuman.com/developer-docs)
- [Sign Up](https://partnerships.ultrahuman.com/)
- [Plans](plans/ultrahuman-plans-pricing.yml)
- [Rate Limits](rate-limits/ultrahuman-rate-limits.yml)
- [Fin Ops](finops/ultrahuman-finops.yml)

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
