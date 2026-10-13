# Preparing reusable public material

Abstract the method into clean files. Do not start by copying an entire private
workspace and deleting obvious secrets afterward.

Keep examples synthetic and self-contained. Replace project-specific names,
paths, hosts, account identifiers, contract addresses, environment names, and
business details with examples unrelated to the source organization. A local
index, log, session transcript, config dump, or Git history can expose information
even when no API key is present.

Review every candidate tracked file, including hidden files, links, archives,
images, and generated metadata. Confirm that references are public sources or
paths inside the distributed skill. Do not embed a private absolute path as an
installation instruction. Public repository links and the intended publisher's
public identity can be retained intentionally.

Inspect the publication diff and staged file list. Scan for known private names
and identifiers without copying that denylist into the public repository. Check
credential patterns and machine-specific paths, but do not treat a clean regex
scan as proof: read the examples, metadata, and claims as well.

Use the intended GitHub account and a suitable public commit identity. Never copy
credentials into a remote URL or commit local authentication files. If publishing
a new independent skill, create clean history rather than inheriting private
commits. Apply a license only to content the publisher has the right to license;
link external sources instead of copying their manuals.

Publishing requires authorization. Once authorized and verified, publish the
intended files, then independently inspect the remote tree and visibility.
Report the usable public URL and any actual limitations, without disclosing the
private project used to derive the method.
