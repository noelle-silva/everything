# Everything

Fast Window v5 registered app for packaged voidtools Everything search.

## Runtime Model

- The app packages official `Everything.exe` and `es.exe` under `vendor/everything/windows-x64/`.
- Build and runtime validation use `vendor-manifest.json` sha256 entries.
- Runtime settings, database and setup state are written under the app data directory.
- Development and release builds use separate app-owned Everything identities so both packages can coexist.
- Development global indexing uses `fast-window-everything-dev` and `Everything (fast-window-everything-dev)`.
- Release global indexing uses `fast-window-everything-release` and `Everything (fast-window-everything-release)`.
- Each channel validates its own service root and fails fast on runtime path mismatches.
- Search runs through the packaged `es.exe` against the app-owned global Everything instance.

## Build

```powershell
npm run vendor:check
npm run build:ui
npm run build:app
npm run build:app:dev
```

## Registration

Register the staged app entry executable from:

```txt
dist-app/v5-windows/package/everything.exe
```

For dev registration use:

```txt
dist-app/v5-windows-dev/package/everything.exe
```

## Verification

```powershell
npm run vendor:check
npm run smoke:runtime
cd backend-go; go test ./...
npm exec -- tsc --noEmit
cargo check --manifest-path src-tauri/Cargo.toml
```
