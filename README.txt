TVDesktop prototype — Apple TV 3,2 / Apple TV Software 7.9

This is an experimental UIKit desktop overlay for the jailbroken Apple TV.
It is not macOS and does not replace Finder or Apple's system preferences.

Build on the Mac:
  cd ~/t/tweak
  ./build.sh

Stage safely over SSH (defaults to root@192.168.0.251):
  ./install.sh [root@APPLE_TV_IP]

The installer first copies any existing DesktopTest files to a timestamped
folder under /var/root/Desktop/TVDesktop-backup-*. It then copies the new
bundle, disabled plist, and assets. It does not enable the tweak or restart
Apple TV.

To enable later, only after the Apple TV is confirmed reachable and stable:
  ./enable.sh [root@APPLE_TV_IP]

To disable injection without deleting the installed files:
  ./disable.sh [root@APPLE_TV_IP]

Neither script reboots or restarts AppleTV. The active plist is what causes
MobileSubstrate to inject the bundle at process launch.

Current prototype features: Finder-style directory browser, 4-item dock,
lazy Safari/WebKit view, System Preferences-style grid, About This MacTV,
arrow/Return/Escape navigation, and viewing the root user's .Trash folder.
Deleting files, launching arbitrary apps, and full Finder behavior are not
implemented. Bluetooth pairing must be done in Apple TV Settings; this app
cannot scan/pair Bluetooth HID devices. Apple TV Software 7.9 app-level mouse
pointer support is unverified and not promised. Graphics acceleration is the
UIKit/Core Animation path provided by the system; there is no custom GPU
renderer or performance guarantee.

The menu bar uses a small wallpaper-matched PNG slice. The dock is centered,
fits its width to its icon count, and touches the bottom screen edge with square
bottom corners. Its tinted glass uses lightweight gradient layers; neither
effect runs a live blur filter or custom shader. Finder sidebar artwork is
rasterized from the supplied Yosemite-era `.icns` files for tvOS/UIKit display.

`Desktop-preview.png`, `System-Preferences-preview.png`, and
`Installer-preview.png` are visual previews. The installer image is a design
mockup; the actual installer remains the command-line shell scripts above.

The source has only been compiled locally for armv7. It has not been tested
on physical Apple TV hardware. Keep the plist disabled until the device is
reachable by SSH and you can recover by running disable.sh.
