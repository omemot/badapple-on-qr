# BA4 QR Real 🍎📷

**Bad Apple!! transmitted through QR codes — frame by frame, in real time.**

A computer converts each monochrome video frame into compressed QR data.
An Android phone scans the rapidly changing QR codes and reconstructs the animation.

- No WebSocket
- No video streaming
- No hidden network transport
- Every QR code contains actual frame data
- Working implementation — not a mockup or template

> The QR codes are the transport.

<!-- Replace with your demo GIF -->
<!-- ![Demo](docs/demo.gif) -->

## Current performance

- Resolution: 32×24
- Frame rate: ~10 FPS
- Compression: Monochrome RLE
- Encoding: Base36
- Sender: Browser
- Receiver: Android Chrome

## Quick Start

```bash
npm install
python -m http.server 8000
```

Sender:
http://localhost:8000/sender.html

Receiver:
http://192.168.x.x:8000/receiver.html

## BA4 Protocol

### Meta QR

```text
M|width|height|fps|title
```

Example:

```text
M|32|24|10|BADAPPLE
```

### Frame QR

```text
F|frame|startColor|base36-rle|fpsx10
```

Example:

```text
F|123|0|g.1.5.2|97
```

- startColor: 0 = black, 1 = white
- fpsx10: FPS × 10

## Roadmap

### BA5

- Dual QR transport
- Left QR = frame n
- Right QR = frame n+2
- Reorder by frame number after decoding
