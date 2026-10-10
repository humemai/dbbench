# Engines

For every engine in every lane, this page states what we run: the version, the container image digest where there is one, every setting that is not the engine's own default, and the reason
for each. The list of engines and their settings is generated from the result rows, so it cannot drift from what was measured.

!!! note "Status"
    The per-engine pages are being written. Until they are published here, each engine's settings are recorded in the benchmark code and on every result row.

## How to tell us a setting is wrong

If a setting we use for your engine differs from what you recommend for this task, open an issue (see [Contribute](contribute.md)) with the engine, the version, the setting, and a link to your documentation.
A corrected configuration is re-run on the same machine and published beside the earlier result, with the reason for the change.
