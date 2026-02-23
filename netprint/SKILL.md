---
name: netprint
description: Register files for convenience store printing (Seven-Eleven via かんたんnetprint, FamilyMart/Lawson via ネットワークプリント). Use when the user wants to print a file or image at a konbini. Returns a reservation number and QR code.
---

# netprint - コンビニプリント登録

## Prerequisites
- **Browser profile:** Always use `profile="openclaw"`

## Pricing (参考)
- 白黒 A4: 20円 / カラー A4: 60円 / カラー A3: 100円 / 写真 L判 (セブンのみ): 40円

## Expiry
予約番号の有効期限: 登録日+1日 (翌日23:59まで)

---

## Flow

### Step 0: Prepare
1. ユーザーに聞く: **「セブン or ファミマ/ローソン？」**
2. 入稿ファイルのパスを確定する（例: `./tmp/<filename>`）。
   - 添付ファイルのローカルパスが取得できるならそのまま使う
   - URLしかない場合のみ `./tmp` にダウンロードする
```bash
mkdir -p ./tmp
curl -L -o ./tmp/<filename> "<url>"
```

---

## Seven-Eleven (かんたんnetprint)

URL: `https://lite.printing.ne.jp/web/`

1. Navigate → snapshot → 「同意する」チェックボックスをクリック
2. Upload: `input[type="file"]` に対象ファイルをアップロード
3. Wait 5秒 → snapshot → **予約番号**をテキストで読み取る
4. 「コンビニでプリントする」ボタンをクリック（**新しいタブ**で `/web/qr` が開く）
5. `browser: tabs` で `/web/qr` タブの targetId を取得
6. そのタブを screenshot → `./tmp/netprint_qr.png`
7. ユーザーに予約番号 + QR画像を送信
8. タブを閉じ、tmpファイルを削除

---

## FamilyMart/Lawson (ネットワークプリント)

URL: `https://networkprint.ne.jp/Lite/start`

1. Navigate → snapshot → 「I agree」ラジオボタンをクリック
2. Upload: `input[type="file"]` にファイルをアップロード（見つからなければ「Select Files」ボタンを先にクリック）
3. Wait 5秒 → snapshot → 「登録」ボタンをクリック
4. 結果画面から**ユーザー番号**を読み取る。QRがあれば screenshot
5. ユーザーにユーザー番号 + QR画像を送信
6. tmpファイルを削除

---

## Output Format

```
🖨️ [店名] プリント登録完了！
予約番号/ユーザー番号: XXXXXXXX
有効期限: YYYY/MM/DD 23:59
[コピー機での操作手順を1行で]
```
