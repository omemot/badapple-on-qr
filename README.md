```
en
```
# BA4 QR Real

Working version. Not a template 🍎📷

## BA4 Specs

Meta QR:

```txt
M|width|height|fps|title
```

Example:

```txt
M|32|24|10|BADAPPLE
```

Frame QR:

```txt
F|frame|startColor|base36-rle|fpsx10
```

Example:

```txt
F|123|0|g.1.5.2|97
```

`startColor` is `0=black`, `1=white`.  
`fpsx10` is `97 = 9.7FPS`.

## Setup

```powershell
npm install
```

## Place frames

```txt
BA4-QR-Real/
├─ frames/
│  ├─ frame_0001.png
│  └─ ...
```

Example to make 64x48 PNGs:

```powershell
mkdir frames
.\YukkuriMovieMaker_v4\Resources\bin\x64\ffmpeg\ffmpeg.exe `
-i .\badapple.mp4 `
-vf "fps=10,scale=64:48:flags=lanczos,format=gray" `
.\frames\frame_%04d.png
```

## Encode

First, 32x24 / 10FPS:

```powershell
$env:OUT_W=32
$env:OUT_H=24
$env:FPS=10
$env:TITLE="BADAPPLE"
npm run encode
```

If you want to go with 64x48:

```powershell
$env:OUT_W=64
$env:OUT_H=48
$env:FPS=10
npm run encode
```

## Start

```powershell
python -m http.server 8000
```

Sender:

```txt
http://localhost:8000/sender.html
```

Receiver:

```txt
http://192.168.x.x:8000/receiver.html
```

If you use HTTP/IP direct access on Android Chrome, for development add:

```txt
chrome://flags/#unsafely-treat-insecure-origin-as-secure
```

Add `http://192.168.x.x:8000`, set to Enabled → restart.

On receiver, if these are true, you’re good:

```js
window.isSecureContext === true
navigator.mediaDevices !== undefined
```

## How to use

1. Open Sender
2. Open Receiver
3. On Receiver, START CAMERA
4. On Sender, scan SEND META
5. On Sender, START

## Next

BA5:
- 2 QRs in parallel
- Left QR: frame n
- Right QR: frame n+2
- Display in the order they are read


```
JP🇯🇵
```
# BA4 QR Real

実働版です。テンプレではありません 🍎📷

## BA4仕様

メタQR:

```txt
M|width|height|fps|title
```

例:

```txt
M|32|24|10|BADAPPLE
```

フレームQR:

```txt
F|frame|startColor|base36-rle|fpsx10
```

例:

```txt
F|123|0|g.1.5.2|97
```

`startColor` は `0=黒`, `1=白`。  
`fpsx10` は `97 = 9.7FPS`。

## セットアップ

```powershell
npm install
```

## framesを置く

```txt
BA4-QR-Real/
├─ frames/
│  ├─ frame_0001.png
│  └─ ...
```

64x48 PNGを作る例:

```powershell
mkdir frames
.\YukkuriMovieMaker_v4\Resources\bin\x64\ffmpeg\ffmpeg.exe `
-i .\badapple.mp4 `
-vf "fps=10,scale=64:48:flags=lanczos,format=gray" `
.\frames\frame_%04d.png
```

## エンコード

まずは32x24/10FPS:

```powershell
$env:OUT_W=32
$env:OUT_H=24
$env:FPS=10
$env:TITLE="BADAPPLE"
npm run encode
```

64x48で攻める場合:

```powershell
$env:OUT_W=64
$env:OUT_H=48
$env:FPS=10
npm run encode
```

## 起動

```powershell
python -m http.server 8000
```

送信:

```txt
http://localhost:8000/sender.html
```

受信:

```txt
http://192.168.x.x:8000/receiver.html
```

Android ChromeでHTTP/IP直アクセスを使う場合は、開発用に:

```txt
chrome://flags/#unsafely-treat-insecure-origin-as-secure
```

に `http://192.168.x.x:8000` を追加し、Enabled → 再起動。

receiverで以下になればOK:

```js
window.isSecureContext === true
navigator.mediaDevices !== undefined
```

## 使い方

1. Senderを開く
2. Receiverを開く
3. Receiverで START CAMERA
4. Senderで SEND META を読ませる
5. Senderで START

## 次

BA5:
- 2QR並列
- 左QRに frame n
- 右QRに frame n+2
- 読めた順に表示

