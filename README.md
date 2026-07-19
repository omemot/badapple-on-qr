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
