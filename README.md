# FiveM JavaScript Builder

Fast and efficient JavaScript obfuscation tool for FiveM resources with intelligent caching.

## Features

- **Smart Caching** - Only rebuilds changed files
- **Parallel Processing** - Multi-core file processing
- **Optimized Obfuscation** - 40% faster while maintaining security
- **Watch Mode** - Auto-rebuild on file changes
- **Multiple Build Types** - Development, Production, and Fast modes

## Quick Setup

1. **Installation:**
   - Dependencies are automatically installed with yarn on first resource start
   - No manual installation required

2. **Create folder structure:**
```
your-resource/
├── html/
│   ├── js/           # Source files (original JS)
│   └── js-load/      # Built files (obfuscated JS)
├── package.json
└── build.js
```

3. **Update fxmanifest.lua:**
```lua
files {
    'html/index.html',
    'html/js-load/*.js'  -- Load built files, not source
}
```

## Commands (In Terminal NOT live console)

```bash
npm run build          # Fast build (optimized obfuscation)
npm run build:dev      # Development (minimal obfuscation)
npm run build:prod     # Production (full obfuscation)
npm run watch          # Watch mode (auto-rebuild)
```

## How It Works

1. **Source Files** - Write your JavaScript in `html/js/`
2. **Processing** - Builder obfuscates and optimizes files
3. **Output** - Processed files go to `html/js-load/`
4. **FiveM Loading** - fxmanifest loads only `js-load/` files
5. **Caching** - Unchanged files use cached versions

## Build Modes

| Mode | Speed | Obfuscation | Use Case |
|------|-------|-------------|----------|
| **Fast** | ⚡ Fastest | Medium | Daily development |
| **Dev** | ⚡⚡ Ultra Fast | Minimal | Testing/debugging |
| **Prod** | 🐌 Slower | Maximum | Production release |

## Performance

- **First Build:** ~1-3 seconds
- **Cached Builds:** ~0.2-0.5 seconds
- **Watch Mode:** Near-instant rebuilds

## Cache System

The builder uses MD5 hashing to detect file changes:
- Cache stored in `html/.build-cache/`
- Only changed files are reprocessed
- Separate cache for dev/prod modes

## File Structure

```
html/
├── js/                 # 📝 Your source files
│   ├── shop.js
│   └── inventory.js
├── js-load/            # 🔒 Built files (auto-generated)
│   ├── shop.js         # (obfuscated)
│   └── inventory.js    # (obfuscated)
└── .build-cache/       # 💾 Cache files
    └── obfuscation-cache.json
```

## Flags

```bash
--dev          # Development mode
--prod         # Production mode  
--watch        # Watch for changes
--no-cache     # Disable caching
--no-parallel  # Disable parallel processing
--help         # Show help
```

## Example Output

```
[0.05s] Cache loaded: 12 entries
[0.12s] CACHE: shop.js
[0.15s] PROD: inventory.js
[0.28s] Build completed in 0.28s!
```

## Tips

- Use **Fast mode** for daily development
- Use **Prod mode** only for releases
- Keep **Watch mode** running while coding
- Source files in `js/` are never loaded by FiveM
- Delete `.build-cache/` to force full rebuild
