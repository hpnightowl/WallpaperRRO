# WallpaperOverlay (RRO for default wallpaper)

This module is a static Runtime Resource Overlay that overrides the framework's default wallpaper drawable.

What it overrides:
- Resource: `@drawable/default_wallpaper` in the `android` package
- File provided: `res/drawable-nodpi/default_wallpaper.png`

How to include in a product build:
1) Add the module to `PRODUCT_PACKAGES` in your product makefile, for example:

   ```PRODUCT_PACKAGES += WallpaperOverlay```
   
3) Build and flash your target product. The APK will be installed to the product partition at:
   `product/overlay/WallpaperOverlay.apk`

4) Verify on device/emulator:
   - `adb shell cmd overlay list | grep WallpaperOverlay` (static overlays under target `android` don't show with a separate package name in some releases).
   - The default wallpaper shown on first boot or when resetting wallpaper should be your image.

Notes:
- This overlay is static (declared with `android:isStatic="true"`) and targets the `android` package.
- Priority is set to 100 so it wins against other product overlays providing `default_wallpaper`.
- Use `drawable-nodpi` so the bitmap is not density-scaled.

Night / large-screen variants
- Large-screen (car) qualifiers:
   - `res/drawable-sw600dp-nodpi/default_wallpaper.png`
   - `res/drawable-sw720dp-nodpi/default_wallpaper.png`
- Night mode:
   - `res/drawable-night-nodpi/default_wallpaper.png`
   - `res/drawable-sw600dp-night-nodpi/default_wallpaper.png`
   - `res/drawable-sw720dp-night-nodpi/default_wallpaper.png`

Provide distinct images if you need different light vs dark wallpapers; otherwise reuse the same file.

Reusing elsewhere:
- Keep this folder under `packages/overlays/WallpaperOverlay`.
- Reference `WallpaperOverlay` in any other product's `PRODUCT_PACKAGES` to reuse.
