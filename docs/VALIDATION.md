# Validation evidence and scope

## Executed for this public reference

- **8 unit tests passed**, including positive and negative paths.
- **5 demonstration checks passed** through the actual domain code.
- Desktop and 390-pixel mobile pages rendered without browser errors or horizontal page overflow.
- The Run demonstration action, three tabs, cross-origin write rejection and unlisted-asset rejection were exercised.
- Manual-only GitHub workflow passed actionlint 1.7.12. No hosted Actions run was consumed for this preparation.
- Trivy 0.75.0 source secret scan: zero findings across the five staged repositories, excluding the Terraform provider cache. This does not prove that arbitrary later additions are secret-free.
- PostgreSQL shell scripts are curated operational-source adaptations. Their shell syntax was checked separately; no real PostgreSQL or cloud restore was run for these screenshots.

See [the machine-readable record](validation-results.json) for date, commands' result counts and domain-source hashes.

## Evidence classification

| Evidence | What it establishes | What it does not establish |
| --- | --- | --- |
| Source-platform narrative | The reusable architecture and operating decisions behind the project | Public access to private records or a copy of the production environment |
| Unit and concurrency tests | Behavior of these exact portable reference modules | Provider permission correctness or distributed multi-region behavior |
| Local screenshots | The running dashboard and real code output with fictional records | A cloud deployment or live Azure/AWS acceptance |
| Scanner source check | No findings from that tool in that selected input | A whole-estate penetration test or vulnerability-free containers |
| Cloud examples | Reviewable configuration/design patterns | Commissioned resources, paid API calls or actual IAM grants |

## Reproduce

```bash
python -B -m unittest discover -s tests -v
python -B -m lab demo
python -B -m lab serve --port 8011
```

The successful screenshots were generated from these local demonstrations; they are not hand-edited success states. The Windows recovery test initially exposed unclosed SQLite handles; explicit connection closure fixed the cleanup failure. Concurrent identity/scan journal tests verify duplicate requests through separate worker connections where relevant.

## Deliberate limits

The public reference does not use real employee records, make paid AI calls, send email/SMS, mutate Microsoft Graph or apply cloud infrastructure. Local filesystem and SQLite tests do not replace provider-specific failure/recovery tests. Real implementation history is described as context and kept separate from reproducible evidence in this repository.
