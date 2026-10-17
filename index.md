<picture><source media="(prefers-color-scheme: dark)" srcset="assets/loomhand-logo-horizontal.svg"><img src="assets/loomhand-logo-mono-navy.svg" alt="loomhand" width="440"></picture>

Computers for AI agents. Each user gets a persistent cloud computer — a
Linux desktop in a microVM — with a resident agent that any model can
drive, plus a native macOS client to watch it, talk to it, and take over.
Local coding agents can use the box through MCP.

```
macOS app / CLI / local agents (MCP)
              │
              ▼
        cocoonbox-api ──► control plane + edge: users, boxes, sharing,
              │           Connect (third-party accounts), vault
              ▼
        sandboxd (cocoonstack/sandbox) ──► warm pools, snapshot, clone
              │
              ▼
        cocoon microVM ── the box
              ├─ Xorg + XFCE desktop
              ├─ cocoonbox-agent ──► agent loop + MCP tools
              └─ toolhost ─────────► cua-driver (loomhand/cua),
                                     desk AT-SPI runtime

  box screen ──► RFB ──► macOS app (loomhand/swift-rfb)
  model calls ──► gw (cocoonstack/gateway)
```

## Projects

- **[cocoonbox](/cocoonbox/)** — the prototype: the in-box agent in Rust,
  the control plane and edge `cocoonbox-api` in Go, the macOS app
  `CocoonBox.app` and the `cocoonbox` CLI in Swift, guest image provisioning, and
  the gRPC contracts.
- **[shuttle](/shuttle/)** — a computer-use host that runs on your own
  machine: local agents drive your desktop over MCP stdio, with your own
  model keys.
- **[swift-rfb](/swift-rfb/)** — an event-driven RFB/VNC client for Apple
  platforms with a Metal renderer.
- **cua** — a fork of [trycua/cua](https://github.com/trycua/cua) carrying
  Linux X11 fixes to `cua-driver`, the screen executor in the box, with the
  fixes sent upstream
  ([repo](https://github.com/loomhand/cua)).

## Built on cocoonstack

loomhand builds on [cocoonstack](https://cocoonstack.github.io/). The
infrastructure stays there; loomhand holds the product and its
client-side libraries.

- **[cocoon](https://cocoonstack.github.io/cocoon/)** — the microVM engine
  every box runs on.
- **[sandbox](https://cocoonstack.github.io/sandbox/)** — `sandboxd` warm
  pools, snapshot and clone; boxes are claimed from it.
- **[gateway](https://cocoonstack.github.io/gateway/)** — the LLM gateway
  (`gw`) that model calls go through.

## Source

Everything lives under
[github.com/loomhand](https://github.com/loomhand).
