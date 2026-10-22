# Photo (mobile) — product

## What it is

A Jetpack Compose Android app shell for a personal photo gallery, plus a
tested pure-Kotlin domain library (`core/`). It is also the canonical Compose
template for the `bookchaowalit-mobile` organisation (see README).

## What exists today

**App (`app/`)** — one activity with a Material 3 bottom navigation bar and
three placeholder screens:

| Screen  | Content today |
|---------|---------------|
| Home    | App title and a one-line description |
| Explore | A static "Explore Photo" label |
| Profile | Owner name and `bookchaowalit.com` |

The screens do not call `core` yet. There is no photo loading (no MediaStore
access, no permissions requested), no network, no backend, no accounts, no
analytics and no persistence.

**Domain library (`core/`)** — pure Kotlin, no Android dependency:

- Image geometry: fit within bounds without upscaling, centred crops for
  1:1 / 4:5 / 16:9 / 3:2, right-angle rotation.
- Justified gallery rows: fixed container width, target row height and gaps,
  rows exactly as wide as the container.
- Timeline grouped by local day (newest first) for a given time zone.
- Album counts with a virtual Favorites album; each photo counted at most once
  per album; blank album names ignored.

Covered by 16 JUnit tests in 3 files under `core/src/test/kotlin/`.

## Distribution

Not published to Google Play or any store. CI builds a debug APK
(`:app:assembleDebug`) only to prove the app compiles; it is not uploaded.

## Not done yet

See [docs/UPGRADE-PLAN.md](docs/UPGRADE-PLAN.md): wire the screens to `core`,
load photos from MediaStore, crop/rotate and save copies, Compose UI tests.
