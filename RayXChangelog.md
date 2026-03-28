## Exact Changes In The Zed Fork

Current diff summary in `D:\Work\projects\RayX.Next\zed`:

- `11` files changed
- `317` insertions
- `66` deletions

Exact modified files:

1. `crates/gpui/src/platform.rs`
   - Removed the `test`/`test-support` gate from `PlatformWindow::render_to_image`
   - Removed the matching gate from the `image::RgbaImage` import

2. `crates/gpui/src/window.rs`
   - Removed the `test`/`test-support` gate from public `Window::render_to_image`

3. `crates/gpui_windows/src/window.rs`
   - Implemented `render_to_image(&self, scene: &Scene) -> anyhow::Result<image::RgbaImage>`
   - Delegates to the DirectX renderer using the current background appearance

4. `crates/gpui_windows/src/directx_renderer.rs`
   - Split render work so scene drawing can be reused without immediate present
   - Added `render_to_image(...)`
   - Added render-target readback through a staging texture
   - Converts BGRA output into RGBA image bytes

5. `crates/gpui_linux/Cargo.toml`
   - Added `image.workspace = true`

6. `crates/gpui_linux/src/linux/x11/window.rs`
   - Implemented `render_to_image(...)`
   - Delegates to the shared WGPU renderer

7. `crates/gpui_linux/src/linux/wayland/window.rs`
   - Implemented `render_to_image(...)`
   - Delegates to the shared WGPU renderer

8. `crates/gpui_wgpu/Cargo.toml`
   - Added `image.workspace = true`
   - Adjusted dependency wiring needed by the new readback path

9. `crates/gpui_wgpu/src/wgpu_renderer.rs`
   - Added runtime image readback support
   - Added helpers to reuse scene encoding for both normal drawing and capture
   - Enabled `COPY_SRC` on the surface texture
   - Copies the rendered texture into a readback buffer and reconstructs an `RgbaImage`

10. `crates/gpui_macos/src/window.rs`
    - Removed the `test`/`test-support` gate from macOS `render_to_image`

11. `crates/gpui_macos/src/metal_renderer.rs`
    - Removed the `test`/`test-support` gate from `render_to_image`
    - Keeps the Metal layer readable by setting `framebuffer_only(false)` for runtime capture too
