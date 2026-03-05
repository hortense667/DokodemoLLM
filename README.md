# DokodemoLLM ver.2.0.3

DokodemoLLM is a Windows tool that lets you select text in *any* application (browser / Word / mail / editor, etc.), press a shortcut, send it to an LLM, and paste the result back in place.
> DokodemoLLM は、どのアプリ（ブラウザ / Word / メール / エディタ等）でも 選択した文章をショートカット一発で LLM に投げて、結果をその場に貼り込めるWindows向けのツールです。

> Note: The Japanese documentation starts after the English section.  
> （日本語の説明は英語による説明の後に記載しています）

(c) 2025, 2026 Satoshi Endo  
https://x.com/hortense667  
https://ascii.jp/serialarticles/1225476/

- The tool itself is **free to use**.
- If you use **OpenAI / Gemini APIs**, you must follow each service’s terms and pricing.  
  **Gemini can be tested with its free API quota**, which is usually enough for everyday text editing / summarizing / translating.

---

## Download (GitHub Releases)

Download the distribution ZIP from GitHub Releases:

```text
https://github.com/hortense667/DokodemoLLM
````

(Open the page → **Releases** → download the latest ZIP)

---

## Quick Start: You only need 2 EXEs + 1 ICO

After extracting the ZIP, you can start using it with:

* **DokodemoLLMahk.exe** — resident launcher (hotkeys / paste-back)
* **DokodemoLLM.exe** — the LLM caller (backend)
* **dokodemollm.ico** — **must stay in the same folder** (do not move/delete)

> A `ソース` (source) folder may also appear after extraction, but it is **not needed for normal users** (it’s for developers/tinkerers).

---

## Setup (fast)

### 1) Extract the ZIP

* Keep the extracted folder structure as-is.
* Make sure **dokodemollm.ico stays in the same folder** as the EXEs.

### 2) Get an API key and set environment variables

You only need **either OpenAI or Gemini** to start.
**A Gemini-free-quota example is shown below**; for typical editing/summarization/translation, the free tier is often enough.

Environment variables:

* For OpenAI: `OPENAI_API_KEY`
* For Gemini: `GOOGLE_API_KEY` (or `GEMINI_API_KEY`)

Optional (only if you want to change the model):

* OpenAI: `OPENAI_MODEL` (e.g. `gpt-4o`)
* Gemini: `GEMINI_MODEL` (e.g. `gemini-2.5-flash`)

#### Where to get API keys (direct links)

```text
OpenAI:
https://platform.openai.com/

Gemini (Google AI Studio):
https://aistudio.google.com/
```

Typical steps:

1. Sign in
2. Create an API key (API Keys / Get API key)
3. Copy the key string
4. Set it as a Windows environment variable

#### Minimal “Gemini free quota” setup (recommended)

* Set only `GOOGLE_API_KEY`
* Optionally set `GEMINI_MODEL=gemini-2.5-flash`
* Start the tool and use it for summarizing / rewriting / translating within the free quota

#### API key safety (important)

* Treat API keys like passwords.
* **Never** paste them into README files, notes, screenshots, videos, or public GitHub repos.
* If you suspect leakage, revoke the key immediately and issue a new one.

> If you set/change environment variables **after launching DokodemoLLM**, you must **exit the tool and launch it again**.
> See **“How to Exit (Important)”** in the Japanese section.

### 3) Launch `DokodemoLLMahk.exe`

* A tray icon appears.
* **First run may take tens of seconds** for internal preparation.
  Because of this, enabling **auto-start** (described later) is recommended.
* After that, use it from any app via hotkeys.

---

## How to Use

1. Select text in any application
2. Press a hotkey
3. Enter a prompt and confirm
4. The result is pasted back

Default hotkeys:

* **Win + Ctrl + O**: OpenAI (GPT)
* **Win + Ctrl + G**: Gemini
* **Ctrl + Win + D**: Local LLM (explained later)

---

## Prompt History

* Stored in `prompt_history.txt`
* Keeps the **most recent 256 entries** (older ones are discarded)
* If you want to remove sensitive or unwanted entries, you may edit/delete `prompt_history.txt` with a text editor.

---

## Auto-start (recommended)

On launch, DokodemoLLM may need **tens of seconds** to be fully ready (especially on first run).
For daily use, set `DokodemoLLMahk.exe` to start with Windows:

1. Press `Win + R`
2. Type `shell:startup` and press Enter
3. Put a shortcut to `DokodemoLLMahk.exe` into that folder

---

## Local LLM (optional)

The hotkey **Ctrl + Win + D** is for a local / internal server that provides an **OpenAI-compatible API**.

Environment variables:

* `LOCALLLM_BASE_URL` (e.g. `http://<IP>:8000/v1`)
* `LOCALLLM_MODEL` (model id exposed by your server)
* `LOCALLLM_API_KEY` (only if required)

Notes:

* **Normally it runs in resident server mode.** The AHK launcher sends requests to the local endpoint.
* Set `<IP>` to the IP address of the machine running your local LLM (check your router, etc.).
* If you want to access it remotely, you can use tools like **Tailscale**:

  * Run `tailscale ip` on the server and use the displayed IP.
  * With this setup, you can use your local LLM while away from home/office as long as you have network access.

---

## Change Hotkeys (requires AutoHotKey) + Rebuild EXE

To change hotkeys, edit `DokodemoLLM.ahk` and rebuild the launcher EXE.

1. Install **AutoHotKey (AHK)** from its official site
2. Edit `DokodemoLLM.ahk` (VS Code recommended)

   * Modifiers:

     * `#` = Win
     * `^` = Ctrl
     * `!` = Alt
   * Examples:

     * `#^o::` → Win+Ctrl+O
     * `#^g::` → Win+Ctrl+G
     * `^#d::` → Ctrl+Win+D
3. Run `build_ahk_exe.bat` to rebuild `DokodemoLLMahk.exe`
4. Exit and re-launch the tool

Build note:

* Avoid building inside synced folders (OneDrive/Dropbox), as file locks may break the build.
* Hotkeys may conflict with other software. If it stops responding, try a different combination.

---

## Credits

* Author / Maintainer: **hortense667**
* Repository: `hortense667/DokodemoLLM` (GitHub)
* Uses:

  * **AutoHotKey** (hotkey resident launcher)
  * **OpenAI API / Gemini API** (depending on your configuration)

---

## Disclaimer

No warranty. The author/contributors are not liable for any damages resulting from use of this software.
I generally cannot respond to individual questions. Since the source code is publicly available, please consider asking the AI or checking the code yourself. In particular, server-side configurations (such as local LLM, vLLM, DGX Spark, etc.) depend on the user's environment, so please resolve these issues on your own.

---

---

# DokodemoLLM（Windows）— README（日本語）

> Note: **英語の説明が前半にあります。**（English section is at the top）

* ツール自体は **無料**で使えます。
* **OpenAI / Gemini API** を使う場合は、各サービスの利用条件・課金体系に従います。
  **Gemini は無料枠で試せる**ので、通常のテキスト編集・要約・翻訳なら無料枠でも十分実用になることが多いです。

---

## ダウンロード（GitHub Releases）

配布 zip は GitHub の Releases からダウンロードできます。

```text
https://github.com/hortense667/DokodemoLLM
```

（上のページ → **Releases** → 最新版 → zip を取得）

---

## 必要なのは「2つの exe」＋「ico」

解凍後、基本は次だけで動きます。

* **DokodemoLLMahk.exe**：常駐（ショートカット受付・貼り込み）
* **DokodemoLLM.exe**：LLM 呼び出し本体（裏側で動く）
* **dokodemollm.ico**：起動時に参照されるため **同じフォルダに置いたまま**（削除・移動しない）

> 解凍すると `ソース` フォルダができますが、**一般ユーザーには不要**です（開発・改造向け）。

---

## 使い始める手順

### 1) zip を解凍する

* 解凍したフォルダ内の構成は **そのまま**で OK です。
* **dokodemollm.ico も同じフォルダに置いたまま**にしてください。

### 2) APIキーを用意して、環境変数に入れる

まずは **OpenAI か Gemini のどちらか1つだけ**で OK です。
なお **Gemini は無料枠のAPIを使う例を説明します**。無料枠でも通常のテキスト編集・要約・翻訳では十分実用になります。

必要な環境変数：

* OpenAI：`OPENAI_API_KEY`
* Gemini：`GOOGLE_API_KEY`（または `GEMINI_API_KEY`）

モデルの設定例：

* OpenAI：`OPENAI_MODEL`（例：`gpt-4o`）
* Gemini：`GEMINI_MODEL`（例：`gemini-2.5-flash`）

#### APIキー入手先（具体的URL）

```text
OpenAI:
https://platform.openai.com/

Gemini（Google AI Studio）:
https://aistudio.google.com/
```

入手手順：

1. 上のページにログイン
2. APIキーを作成（API Keys / Get API key など）
3. キーをコピー
4. Windows の環境変数に貼り付け

#### Gemini 無料枠で試す最小例

* `GOOGLE_API_KEY` だけ設定して試す
* 必要なら `GEMINI_MODEL=gemini-2.5-flash` を設定
  → 要約・翻訳・リライトなどが軽快に動きます（無料枠の範囲で）

#### APIキー取り扱いの注意（重要）

* APIキーは **パスワードと同等**です。
* README、メモ、スクリーンショット、動画、公開リポジトリに **貼らない**でください。
* 漏えいが疑われたら、キーを無効化して作り直してください。

> **環境変数を、このソフト起動後に設定・変更した場合**：
> いったん **DokodemoLLM を終了してから起動し直してください**。
> 終了の仕方は後半の **「ソフトの終了の仕方」** を必ずご覧ください。

### 3) DokodemoLLMahk.exe を起動する

* タスクトレイにアイコンが出ます。
* **初回のみ**、内部的な準備のために **数十秒かかる**ことがあります。
  そのため、通常は **自動起動（後述）**がおすすめです。

---

## 使い方

1. 文章を範囲選択
2. ショートカットを押す
3. プロンプト入力 → 実行
4. 結果が貼り込まれる

既定のショートカット：

* **Win + Ctrl + O**：OpenAI（GPT）
* **Win + Ctrl + G**：Gemini
* **Ctrl + Win + D**：ローカルLLM（後述）

---

## 履歴（prompt_history.txt）

* 入力したプロンプトの履歴が `prompt_history.txt` に保存されます。
* 保存されるのは **直近までの 256 件**です（古いものから消えます）。
* 都合のわるい履歴は、テキストエディタなどで `prompt_history.txt` を編集・削除してもよいでしょう。

---

## 自動起動（おすすめ）

起動後に内部処理が整うまで **数十秒かかる**ことがあります（初回は長めになることもある）。
普段使いなら Windows 起動時に自動起動がおすすめです。

1. `Win + R`
2. `shell:startup` → Enter
3. 開いたフォルダに **DokodemoLLMahk.exe のショートカット**を入れる

---

## ローカルLLM（任意）

**Ctrl + Win + D** は、OpenAI互換APIの **ローカルLLM / 社内サーバ**向けです。

環境変数：

* `LOCALLLM_BASE_URL`（例 `http://<IP>:8000/v1`）
* `LOCALLLM_MODEL`
* `LOCALLLM_API_KEY`（必要な場合のみ）

補足：

* IP は、ルーターなどからローカルLLMを立ち上げたサーバーの IP アドレスを設定してください。
* Tailscale などを使ってリモートからアクセスしたい場合は、サーバー上で `tailscale ip` のコマンドで表示された IP アドレスを設定してください。
  つまり、出先からでもネット環境があればローカルLLMが使えます。

---

## ショートカットを変更する方法（AutoHotKeyが必要）＋exe再作成

ショートカットを変えたい場合は `DokodemoLLM.ahk` を編集し、**AutoHotKey を使って再度 exe 化**します。

1. **AutoHotKey（AHK）** を公式サイトからインストール
2. `DokodemoLLM.ahk` をエディタで開いてホットキー定義を変更

   * 記法の目安：

     * `#` = Win
     * `^` = Ctrl
     * `!` = Alt
   * 例：

     * `#^o::`（Win+Ctrl+O）
     * `#^g::`（Win+Ctrl+G）
     * `^#d::`（Ctrl+Win+D）
3. `build_ahk_exe.bat` を実行して `DokodemoLLMahk.exe` を作り直す
4. ソフトを終了 → 起動し直す

注意：

* OneDrive/Dropbox 等の同期フォルダ直下でのビルドは避けてください（ロックで失敗することがあります）。
* ショートカットは他ソフトと衝突することがあるので、反応しない場合は別の組み合わせにしてください。

---

## ソフトの終了の仕方（重要）

環境変数の設定変更後や、反応がおかしい時は **いったん終了して再起動**してください。

### タスクマネージャから終了

1. `Ctrl + Shift + Esc` → タスクマネージャ
2. `DokodemoLLMahk.exe` / `DokodemoLLM.exe` を探す
3. **タスクの終了**

---

## クレジット

* Author / Maintainer: **hortense667**
* GitHub: `hortense667/DokodemoLLM`
* 使用技術：

  * **AutoHotKey**（常駐ホットキー）
  * **OpenAI API / Gemini API**（設定に応じて利用）

---

## 免責

本ソフトウェアの利用によりユーザーが被った損害について、作者・貢献者は一切補償しません。
個別の質問には基本的にお答えできません。ソースコードが公開されているため、AIに聞く、あるいはコードを自身で確認することを検討してください。
とくにサーバー側の設定（ローカルLLM・vLLM・DGX Spark など）はユーザーの環境に依存するため、自身で解決してください。

