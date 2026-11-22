# SA PSD Runner

Private-payload processing runner for the SA / SpineAnimator pipeline.

This repository is intentionally public and must contain **no source artwork, PSD files, source bundles, credentials, or private project data**.

## Original source handoff

The `Import original source bundle` workflow accepts:
- an HTTPS URL to the exact ZIP payload (the URL must be reachable by GitHub-hosted runners);
- the expected SHA-256 digest;
- the target branch in `SpineAnimator/spine-animator-private`.

It downloads the ZIP, verifies its SHA-256, checks ZIP integrity, and uploads it to the private target repository using the `SA_TARGET_REPO_TOKEN` Actions secret. The token must be a fine-grained token restricted to `SpineAnimator/spine-animator-private` with Contents: Read and write. It is never stored in this repository's source.

The workflow fails closed if the URL, digest, secret, ZIP integrity, or target branch update is invalid. It does not create or use pull requests.

## Important limitation

This runner does not magically expose files from a ChatGPT/container session. A reachable HTTPS source URL is required for the workflow to fetch the ZIP. Do not use public file hosting for private source artwork. Prefer a short-lived, private, authenticated download URL supported by the hosting provider.
