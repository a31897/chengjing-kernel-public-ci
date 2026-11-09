# Experimental Chromium Privacy Kernel CI

Open-source patch overlays and generic rendering regression tests. This is not
a validated release and does not promise anonymity.

- Upstream: https://github.com/aliasmode/aliasmode-chromium at
  9f6679274b7e87c943b28104921b1a8d6bc30666, Chromium 155.0.8059.85.
- 0174 removes a positive-size readback cutoff. 0176 makes explicit Canvas/WebGL
  restrictions cover workers. 0177 separates image-only policy from font/audio
  umbrella noise. 0178 bounds Windows ThinLTO workers to two; it is build
  infrastructure, not a privacy fix.
- No proprietary browser code, user profile, credential, proxy configuration,
  local capture, or screenshot is included.
- `source-bundle.zip` contains generic source inputs with a SHA-256 sidecar and
  per-file digests. It is a source bundle, not an executable.
- Pixel provenance, full Canvas/WebGL correctness, and actual WebGPU output
  independence remain unimplemented/unverified. Tests retain those failures.
- CI uses only the approved public repository and standard Windows 2022 hosted
  runners. No billing, cache quota, or paid runner settings are changed.
- The previous cold 2-job build stopped after 350 minutes at 27,735/58,405 tasks.
  The revised plan uses at most four compiler jobs, a hash-pinned 8 GB compiler
  cache, a real cached/direct object control, and up to three bounded compile
  slices. A deliberate budget checkpoint, useful measured cache statistics and
  confirmation of cache persistence are required before a subsequent slice.
- Official optimization, PGO, ThinLTO and browser features remain enabled.
  Finite cache eviction and link memory can still prevent completion. A cache
  handoff is not blind reuse of an old browser or independent reproducibility
  verification. See `ci/BUILD-PLAN.md` inside the bundle.
- No candidate is automatically adopted by an installed manager. Actual
  browser probes have no CDP/getter overrides. They check 96 known-pixel cases,
  whole and byte-split WebGL2 PBO reads, worker agreement, reload/restart,
  distinct profiles and explicit native access restrictions. Headless CI is
  not a substitute for a headed real-GPU desktop test.

Derived native changes follow the upstream GPL-3.0 license included in LICENSE.
See kernel/README.md and the overlay notes inside the bundle for validation
boundaries. Successful compilation alone does not establish isolation.

