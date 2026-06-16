# Tracenil

**Remove EXIF metadata from your photos — entirely in your browser.**

Every photo your phone or camera takes carries hidden metadata: the GPS coordinates where it was shot, your device make and model, the exact timestamp. When you share that photo online, the metadata usually travels with it. Tracenil strips it out.

The catch with most "private" tools is that you have to *trust* them. Tracenil is built so you don't have to.

🔗 **Live:** https://tracenil.com

---

## Why you can trust it

Most privacy tools say "we process everything locally." You have no way to check. Tracenil is built so the claim is verifiable, not just stated:

- **Watch the network.** Open your browser's dev tools (F12) → Network tab, then scrub a photo. No request carries your image anywhere. Nothing is uploaded.
- **Pull the plug.** Load the page, then turn off your internet. It still works — because all processing happens on your device.
- **Read the code.** The entire tool is the single `index.html` file in this repo. No frameworks, no trackers, no build step, no dependencies. You can read every line in a few minutes.

That last point is the whole design philosophy: **one file, zero dependencies.** There is nowhere for anything to hide.

---

## How it works

- Reads your image locally with the browser's `FileReader`.
- Parses EXIF tags (GPS, device, lens, timestamp, orientation) with a small hand-written parser — no third-party library.
- Strips all metadata by re-encoding the image through an HTML `<canvas>`, which carries no metadata across.
- Preserves the original orientation by baking the EXIF orientation tag into the pixels before stripping, so the clean copy is never rotated.
- Verifies the result by re-parsing the cleaned file and confirming no EXIF remains.

Supported formats: **JPEG, PNG, WebP.**

---

## Run it yourself

No build step. Clone and open:

```bash
git clone https://github.com/tracenil/tracenil.git
cd tracenil
open index.html        # or just double-click the file
```

That's it. There is nothing to install.

---

## Privacy

Tracenil does not upload, store, log, or transmit your images. There is no server, no analytics, and no third-party scripts. Your photos never leave your device. See [PRIVACY.md](PRIVACY.md) for the full statement.

---

## License

[MIT](LICENSE) — free to use, modify, and learn from.

---

## Roadmap

Tracenil starts with EXIF removal, but the direction is on-device privacy tooling more broadly — all processed locally, all verifiable:

- On-device face blur
- Document / screenshot redaction (masking personal details)
- Showing *why* something was flagged, not just hiding it

Issues and ideas welcome.
