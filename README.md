# ChatRecap downloads

Public, static distribution site for ChatRecap. The application source remains in a separate private repository.

- Website: https://hochipants.github.io/wrapped-downloads/
- Mac setup: https://hochipants.github.io/wrapped-downloads/mac-setup/
- Windows setup: https://hochipants.github.io/wrapped-downloads/windows-setup/
- Privacy: https://hochipants.github.io/wrapped-downloads/privacy/
- Android privacy: https://hochipants.github.io/wrapped-downloads/android-privacy/
- Support: https://hochipants.github.io/wrapped-downloads/support/
- App Review sample: https://hochipants.github.io/wrapped-downloads/samples/wrapped-review-sample.csv

`downloads/ChatRecap-for-Mac.zip` is replaced automatically after a Mac build is signed, accepted by Apple's notarization service, and stapled by the private build workflow.

`downloads/ChatRecap-for-Windows.exe` and its SHA-256 checksum are replaced automatically by tagged Windows builds from the private build workflow.

Legacy installer URLs remain available for existing app versions. The Mac companion is signed and notarized under its ChatRecap name; the Windows companion uses ChatRecap branding and remains an unsigned beta.


## Video previews for Messages

App landing pages include static Open Graph video metadata and a player with no autoplay or eager media download. The MP4 is a direct public HTTPS asset; the poster remains available as an image fallback. Legal pages retain their own previews.

`link-previews.json` is the app preview catalog. To update a clip, use a new versioned asset filename, update its dimensions, duration and file sizes in the catalog, then run:

```sh
python3 scripts/link-previews.py --write --probe
```

Use H.264, yuv420p, a fast-start MP4, and a poster at least 900 pixels wide. Keep the video, poster and icons together below 10 MB; this validator reserves 100 KB for icons. Metadata must be in the initial HTML and must not depend on JavaScript. Use only approved footage or sample screenshots without private names, conversations, account details or secrets. Screenshot montages are labeled as screen captures.

Before publication, run `python3 scripts/link-previews.py --probe` and `git diff --check`. After publication, run `python3 scripts/link-previews.py --live` to check exact live HTML, MIME types, sizes and MP4 byte-range support. `--probe` additionally requires FFprobe.

Apple controls autoplay, caching and presentation in Messages. These checks verify the website and media, not delivery or autoplay in a conversation. This metadata applies to these website links; Apple controls the separate App Store and TestFlight link previews.

References: [Apple TN3156](https://developer.apple.com/documentation/technotes/tn3156-create-rich-previews-for-messages) and [Open Graph](https://ogp.me/).
