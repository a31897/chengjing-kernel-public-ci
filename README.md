# Experimental Chromium Privacy Kernel CI

Open-source patch overlays and generic rendering regression tests. This is not a validated release and does not promise anonymity.

- Upstream: https://github.com/aliasmode/aliasmode-chromium at 9f6679274b7e87c943b28104921b1a8d6bc30666, Chromium 155.0.8059.85.
- 0174 removes a positive-size readback cutoff. 0176 makes explicit Canvas/WebGL restrictions cover workers. 0177 separates image-only policy from font/audio umbrella noise.
- No proprietary browser code, user profile, credential, proxy configuration, local capture, or screenshot is included.
- source-bundle.zip contains the complete generic inputs with a SHA-256 sidecar and per-file digests. It is a source bundle, not an executable.
- Pixel provenance, full Canvas/WebGL correctness, and actual WebGPU output independence remain unimplemented/unverified. Tests intentionally retain those failures.
- Windows Actions use standard hosted runners only. Resource gates do not enable paid runners. No built artifact is automatically adopted by an installed manager.
- CI runs actual browser programs without CDP/getter overrides, checks 96 known-pixel cases, worker agreement, reload/restart, distinct profiles, and explicit native access restrictions. Headless CI is not a substitute for a headed real-GPU desktop test.

Derived native changes follow the upstream GPL-3.0 license included in LICENSE. See kernel/README.md and the overlay notes inside the source bundle for validation boundaries.
