# mpv-build-macOS
A set of scripts that help build [mpv](https://mpv.io) with [MoltenVK](https://github.com/KhronosGroup/MoltenVK) support.  

### Requirements

- [Xcode.app](https://developer.apple.com/xcode/)
- [Homebrew](https://brew.sh)

### Build and install

1. Make sure Xcode is ready by running:  

   ```sh
   xcodebuild -runFirstLaunch
   ```

2. Clone the repository:  

   ```sh
   git clone "https://github.com/m154k1/mpv-build-macOS.git"
   cd mpv-build-macOS
   ```

3. Install dependencies from Homebrew:  

   ```sh
   xargs brew install --formula < homebrew/build-deps.txt
   ```

4. Create an installation directory for local packages:  

   ```sh
   sudo mkdir /opt/local
   sudo chown "$USER":admin /opt/local
   mkdir /opt/local/stow
   ```

5. Fetch sources:  

   ```sh
   ./fetch all
   ```

6. Build mpv and its dependencies:  

   ```sh
   # This will build and install mpv as CLI program
   ./build-all

   # Alternatively, you can make an app bundle by adding '--bundle' option
   # This will create mpv.tar.gz with mpv.app
   ./build-all --bundle
   ```

7. Add `/opt/local/bin` to your `$PATH`.

### Recommended settings

```cfg
# ~/.config/mpv/mpv.conf
vo=gpu-next
hwdec=yes
macos-render-timer=feedback
```

### Environment variables

- `MTL_HUD_ENABLED=1`  
  Enables the [Metal Performance HUD](https://developer.apple.com/documentation/xcode/monitoring-your-metal-apps-graphics-performance).  

- `MVK_CONFIG_LOG_LEVEL=3`  
  Enables verbose MoltenVK logging.  
