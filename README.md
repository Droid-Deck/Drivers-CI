# DroidDeck Drivers

Downloads for DroidDeck's Turnip drivers. Each release carries:

- `DD-Turnip-vX.Y.Z.zip`: the Android driver (`android/`) and the Linux ARM64 driver (`linux/`), indexed by `manifest.json`, with `NOTICE` and `LICENSES/`
- `DD-Turnip-vX.Y.Z.zip.sha256`
- `DD-Turnip-vX.Y.Z-source.tar.xz`: the Corresponding Source, Mesa at the built commit and the patches and build scripts that produced the drivers

The drivers are Mesa (MIT) with a patch set under the GNU General Public License version 3.

DroidDeck lists these under Components → GPU drivers → Manual, or import a downloaded zip there with **Import .zip**.

## Auto picks

`auto-drivers.json` tells DroidDeck's Auto mode which driver pair to use on each GPU. DroidDeck reads it from
`main` whenever it checks for driver releases, so editing it changes Auto for everyone without an app release.
If the file is missing or doesn't parse, the app uses its built-in table (the same rules as the first version
of this file).

- The first rule that matches the GPU wins. A rule matches `families` (`A6XX`, `A7XX`, `A7XX_LOW`, `A8XX`,
  `ADRENO_UNKNOWN`) and optionally `models` (exact Adreno numbers), `oneUi8Gen2`, `minSdk`, and
  `blobMin`/`blobMax` (the Qualcomm system driver version, e.g. `676` from `512.676.0`; a rule with a blob
  range never matches when the app can't read it).
- `prefer` lists pair keys in order: `dd-turnip` (newest DD-Turnip), `banner`, `banner-a8xx`,
  `banner-8g2-oneui`, `banner-710-720-test`, `wn-b`, `wn-p`. Auto takes the first one that's published as a
  complete pair and hasn't failed on that device. A build that never gets a session to start is rolled back
  and skipped there, so the next preference acts as the fallback.
- Only pair keys go here. Download URLs and checksums always come from the GitHub releases.
