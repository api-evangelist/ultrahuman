# Ultrahuman (ultrahuman)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
