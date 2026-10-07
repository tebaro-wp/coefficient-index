# Tebaro Source Policy

The public Tebaro coefficient feed is deliberately separated from private source acquisition.

## Eligibility principles

Private collector inputs should be used only when their use is authorized or otherwise permitted under the applicable terms and law. Operational policy includes:

- review source terms and access conditions;
- prefer documented APIs, feeds, or written permission where available;
- respect reasonable rate limits and caching opportunities;
- use minimal collection frequency necessary for the calculation;
- do not bypass login requirements, CAPTCHA, paywalls, anti-bot controls, or other access restrictions;
- do not misrepresent access as a human user where automated access is prohibited;
- suspend or remove a source when a credible rights/terms concern is raised while it is reviewed;
- retain only the private operational data needed for reliability, auditing, and safety.

## Public-output boundary

The public feed does not expose:

- provider/source names;
- source URLs;
- raw observations;
- per-currency market values;
- scrape logs.

Publishing only a scalar coefficient does not create permission to acquire private inputs. Source authorization remains an independent obligation.

## Privacy boundary

The collector and public feed must not require or transmit customer, order, product, personal, analytics, or telemetry data for coefficient calculation.
