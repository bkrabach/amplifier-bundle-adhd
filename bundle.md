---
bundle:
  name: adhd
  version: 0.1.0
  description: ADHD-shaped output style — /adhd mode plus opt-in always-on
    behavior. Port of github.com/ayghri/i-have-adhd (MIT).

includes:
  - bundle: git+https://github.com/microsoft/amplifier-foundation@main
  - bundle: git+https://github.com/microsoft/amplifier-bundle-modes@main
---

# adhd

Activate with `/adhd` for accessible, action-oriented output: answer first,
numbered instructions when needed, and concise progress reports. The style
adapts to the reader; it does not add approval gates or return authorized work
to them.

Say "stop adhd mode" or use `/mode off` to deactivate.

For always-on shaping (no mode toggle needed), compose
`adhd:behaviors/always-on` into your bundle or app configuration.

---

@foundation:context/shared/common-system-base.md
