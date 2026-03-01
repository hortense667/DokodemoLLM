# DokodemoLLM ver.2.0.0

あらゆるアプリケーションからLLM（OpenAIのGPTとGemini）を呼び出せるソフトウェアです。
This software allows you to call LLM (OpenAI GPT and Gemini)  from within any application.  

(c) 2025, 2026 Satoshi Endo 
https://x.com/hortense667
https://ascii.jp/serialarticles/1225476/

Note: 日本語の説明は英語による説明の後に記載しています。

## Overview
This software allows you to call LLMs (OpenAI GPT, Google's Gemini, and compatible local/network LLM servers such as DGX Spark) and input the results in most Windows software where text input is required.

## Usage Instructions

1. **Execute DokodemoLLMahk.exe**  
   Obtain an API key from OpenAI or Gemini and set it as an environment variable. Then, simply unzip the distribution package and execute DokodemoLLMahk.exe. An icon will appear in the system tray.

2. **How to Call LLM**  
   2-1. Select Text in Input Area  
   First, select the text you want to process in the input or editing area of applications like Gmail, Word, or text editors.

   2-2. Input Prompt  
   Use `Win-Ctrl-o` to call OpenAI GPT, `Win-Ctrl-g` for Gemini, or **`Ctrl-Win-d`** for DGX / local LLM. The UI (in English) consists of:
   - A **dropdown list** of prompt history and a **multi-line editor** for the prompt.
   - **Temperature** (0.0–2.0) and **top_p** (0.0–1.0) sliders in one row; defaults depend on the model (e.g. GPT/Gemini 0.7, DGX 0.2 for temperature; top_p default 1.0).
   - A **hint line** below the sliders (translation/summary vs. variation, and when to lower top_p if output is too random).
   - **Reset to default**: When the current temperature/top_p differ from the selected model’s default, a red “Reset to default” button appears; click it to restore the model’s default values.
   - Buttons: **OK**, **Cancel**, **Clear**.

   For the first prompt, type in the editor and press "OK". You can pick a previous prompt from the dropdown; they are listed most-recent first. The selected prompt is shown in the editor for editing. Prompt history is saved in "prompt_history.txt" (up to 256 entries). Each entry stores the prompt plus **temperature**, **top_p**, and the **model name** (e.g. gpt-4o, gemini-2.5-flash, nvidia/Llama-3.3-70B-Instruct-FP4). When you choose a history item, if the stored model name matches the model you are using now, the stored temperature and top_p are restored; otherwise the current model’s defaults are used.

   Examples: "Summarize", "Proofread the following", "Translate to English", or multi-line prompts.  
   Note: Appending "/w" at the end of a prompt runs a web search and uses the first 1000 characters from the top 3 sites as context.

3. **Confirm Content**  
   After a few seconds or up to several tens of seconds, a window will appear asking **"Use this result?"**  
   - **Yes**: Replaces the selection with the result  
   - **No**: No changes  
   - **Cancel**: Appends the result to the original text.

4. **Errors**  
   If the API returns a quota error (e.g. OpenAI 429 / insufficient_quota), a short message is shown suggesting you check plan and billing or try again later. Other LLM errors are shown with an "LLM error:" prefix.

## Necessary Settings for Operation

1. **Set Environment Variables**  
   - **OpenAI API Key**  
     Obtain an OpenAI API key and set the following environment variable:  
     `OPENAI_API_KEY`  
     Optionally set `OPENAI_MODEL` (default: `gpt-4o`) to use a different model.
   - **Google API Key**  
     Obtain a Gemini API key and set the following environment variable:  
     `GOOGLE_API_KEY`  
     Optionally set `GEMINI_MODEL` (default: `gemini-2.5-flash`) to use a different model.
   - **DGX / local LLM (for Ctrl-Win-d)**  
     When using a local or network LLM server (e.g. vLLM on NVIDIA DGX Spark) that provides an OpenAI-compatible API, set:  
     `LOCALLLM_BASE_URL`, `LOCALLLM_MODEL`, and optionally `LOCALLLM_API_KEY`. See the section "Using Local LLM (DGX Spark)" for details. 
     Note: Local mode was previously implemented in a fork by fugahoge, but since the code was rewritten in C#, this Python version introduces it as a new feature. The speed-up approach also draws from fugahoge's method.

   Note: You can set only the one you want to use, or multiple if you want to use them.

2. Unzip DokodemoLLM.zip  
   Download dokodemollm.zip from the "Releases" section of the DokodemoLLM repository. Unzip it to an appropriate folder. DokodemoLLMahk.exe is included in the extracted folder. Leave the dist folder and its contents in the same folder where you execute DokodemoLLMahk.exe.

3. **Register for Auto Execution**  
   Register a shortcut to DokodemoLLMahk.exe in the Windows startup menu.

## Changing Shortcuts
If you want to change the shortcuts (`Win-Ctrl-o`, `Win-Ctrl-g`, or `Ctrl-Win-d`), modify DokodemoLLM.ahk in the source folder. In this case, you need to have AutoHotKey installed and running. Currently, the settings are as follows:
- "^#o::" launches with Ctrl-Win-o: OpenAI GPT (model from env var `OPENAI_MODEL`, default gpt-4o)
- "^#g::" launches with Ctrl-Win-g: Gemini (model from env var `GEMINI_MODEL`, default gemini-2.5-flash)
- "^#d::" launches with **Ctrl-Win-d**: DGX / local LLM (model from env var `LOCALLLM_MODEL`)

## Usage on Mac
1. **Prepare a Snippet Tool Other than AutoHotKey**  
   Use an appropriate snippet tool to create a script that calls DokodemoLLM.py. Therefore, a Python environment is required. The snippet tool passes the prompt to DokodemoLLM.py via clipboard, and the result is returned to the snippet tool via clipboard as well. Please see the source code for details.

## Disclaimer

The authors and contributors of this software do not compensate for any damage or loss that users may suffer from using it. We are generally unable to answer individual questions or provide support. Since the source code is available, asking an AI or consulting the code yourself is one option. In particular, server-side configuration (e.g. local LLM, vLLM, DGX Spark) depends on your environment; please resolve such issues on your own.


## 概要
Windowsのほとんどのソフトウェアのテキストを入力するシーンでLLM（OpenAI GPT、GoogleのGemini、およびDGX Sparkなどのローカル／ネットワークLLM）を呼び出して結果を入力できるソフトウェアです。

## 使い方の手順

1. **DokodemoLLMahk.exeの実行**  
OpenAI、たまは、GeminiのAPIキーを取得して環境変数に設定してください。あとは、配布パッケージのzipを解凍してDokodemoLLMahk.exeを実行するだけ。トレイにアイコンが現れます。

2. **LLMの呼び出し方**  
2-1. テキスト入力エリアで範囲選択  
まず、Gmail、Word、テキストエディタなどの入力・編集画面で処理対象にしたい部分を範囲選択します。

2-2. プロンプトの入力  
`Win-Ctrl-o`でOpenAIのGPT、`Win-Ctrl-g`でGemini、**`Ctrl-Win-d`**でDGX／ローカルLLMが呼び出されます。

UIは英語表示で、次の要素があります。
- **ドロップダウン**（履歴）と**複数行エディタ**（プロンプト入力）
- **Temperature**（0.0～2.0）と **top_p**（0.0～1.0）のスライダーが1行に並ぶ（モデルごとの既定値：GPT/Gemini は temperature 0.7、DGX は 0.2；top_p は既定 1.0）
- スライダー下の**ヒント**（翻訳・要約時は低めの temperature、バリエーション出したいときは高め；発散しすぎる場合は top_p を下げる、など）
- **Reset to default**：現在の temperature／top_p がそのモデルの既定値と異なるときだけ赤い「Reset to default」ボタンが表示され、押すと既定値に戻る
- ボタン：**OK**、**Cancel**、**Clear**

初めてのプロンプトはエディタに入力して「OK」を押してください。過去のプロンプトはドロップダウンから選べます（直近使用順）。選んだプロンプトはエディタに表示されるので編集して使えます。プロンプトが決まったら「OK」をクリックします。

履歴は「prompt_history.txt」に最大256件まで保存されます。**各履歴にはプロンプトに加え、temperature・top_p・使用したモデル名（例: gpt-4o, gemini-2.5-flash, nvidia/Llama-3.3-70B-Instruct-FP4）が保存されます。** 履歴を選んだとき、保存時のモデル名と今使うモデルが同じなら保存された temperature／top_p が復元され、異なるモデルならそのモデルの既定値が使われます。

例：「Summarize」「Proofread the following」「英訳して」「誤字チェック」など。改行を含む複雑なプロンプトも入力できます。  
※プロンプトの末尾に「/w」をつけると Web 検索し、上位3サイトの冒頭1000文字を参考に答えます。

### ローカルLLMモード（Ctrl-Win-d）

OpenAI互換APIを提供するローカル／ネットワークサーバー（例：NVIDIA DGX Spark上のvLLM）を使う場合は、**Ctrl-Win-d** で呼び出せます。環境変数 `LOCALLLM_BASE_URL` と `LOCALLLM_MODEL` を設定してください（`LOCALLLM_API_KEY` は任意）。詳細は下記「ローカルLLM（DGX Spark）を使う場合（詳細）」を参照してください。
なおローカルモードは、fugahogeさんによるforkで実現されていましたが、コードがc# に書き換えられていたためPython版のこちらは新なフィーチャーと実装することとしました。また、高速化に関してもfugahogeさんのアプローチを参考にさせていただいています。

3. **内容確認**  
数秒から数十秒が経過すると **「Use this result?」** のウィンドウが表示されます。  
- **Yes**：選択範囲が結果で置き換え  
- **No**：変更なし  
- **Cancel**：元の文の後に結果が追記されます。

4. **エラー表示**  
API のクォータ超過（OpenAI の 429 / insufficient_quota など）のときは、プラン・請求の確認や時間をおいて再試行する旨の短いメッセージが表示されます。その他の LLM エラーは「LLM error:」を付けて表示されます。

## PyInstaller で exe 化して使う

Python をインストールしたくない場合や、配布しやすくするために exe 化できます。

1. **ビルド**  
   同じフォルダで `build_exe.bat` を実行します（日本語を避けたメッセージで、アイコンなし spec を使い Dropbox 等でのロックエラーを防ぎます）。
   ```powershell
   pip install pyinstaller openai google-generativeai pyperclip requests beautifulsoup4
   build_exe.bat
   ```
   または手動で: `pyinstaller --noconfirm --clean DokodemoLLM.spec`  
   `dist\DokodemoLLM.exe` ができます。Dropbox 等の同期フォルダで WinError 110 が出る場合は、`dist` をローカルドライブに変えるか、生成した exe を別フォルダにコピーしてから使ってください。

2. **AutoHotkey 側の設定**  
   - **推奨**: `DokodemoLLM.exe` を `DokodemoLLM.ahk` と同じフォルダに置く。AHK は同じフォルダの `DokodemoLLM.exe` を自動で使います。
   - **別フォルダに置く場合**: ユーザー環境変数 `DokodemoLLM_Exe` に exe のフルパスを設定（例: `C:\Tools\DokodemoLLM.exe`）。

3. **常駐の起動**  
   exe を使う場合、AHK が初回にサーバー未起動を検知すると自動で `DokodemoLLM.exe serve` を起動します。事前に手動で起動したい場合は `DokodemoLLM.exe serve` を実行してください。

4. **API キー**  
   exe 化しても環境変数（`OPENAI_API_KEY` / `GOOGLE_API_KEY` など）はそのまま必要です。AHK と同じ環境で exe を動かせば同じ変数が参照されます。

## AHK を exe 化してスタートアップで起動

AutoHotkey を入れていない PC でも動かしたり、ログイン時に自動で起動させたい場合は、AHK を exe にコンパイルしてスタートアップに登録します。

1. **前提**  
   - ビルド時だけ **AutoHotkey v2** がインストールされている必要があります。  
   - 出力する **DokodemoLLMahk.exe** は「AHK のランチャー」用です。Python 常駐用の **DokodemoLLM.exe** とは別ファイルです。

2. **ビルド**  
   同じフォルダで `build_ahk_exe.bat` を実行します。
   ```batch
   build_ahk_exe.bat
   ```
   - 同じフォルダに **DokodemoLLMahk.exe** ができます。  
   - `DokodemoLLM.ico` があれば exe のアイコンに使います。  
   - Ahk2Exe が見つからない場合は、AutoHotkey v2 をインストールするか、環境変数 **AHK2EXE_PATH** に `Ahk2Exe.exe` のフルパスを設定してください。

3. **スタートアップに登録**  
   - `Win + R` → `shell:startup` → Enter でスタートアップフォルダを開く。  
   - `DokodemoLLMahk.exe` のショートカットを作成し、そのフォルダに置く（または exe を直接コピー）。  
   - これでログイン時にトレイで DokodemoLLM が起動し、Ctrl+Win+o / g / d が使えます。

4. **フォルダ構成の目安**  
   スタートアップからは「ショートカット」で起動するのが一般的です。ショートカットの「作業フォルダ」は exe と同じフォルダにしておくと、`prompt_history.txt` や `DokodemoLLM.exe`（Python 側）の参照が安定します。exe を別の場所に移した場合は、そのフォルダに `DokodemoLLM.exe`（と必要なら `prompt_history.txt`）も一緒に置いてください。

## Python常駐モード（高速化）

毎回Pythonを起動せず、**常駐サーバーにHTTPで依頼**するため、応答が速くなります（起動・importは1回だけ）。

- **自動**: 初回にショートカットを押すと、サーバーが未起動なら自動で `DokodemoLLM.py serve` が起動し、約5秒後に再試行します。
- **手動で常駐させたい場合**: あらかじめ次を実行しておくと、初回からすぐに依頼できます。  
  `python DokodemoLLM.py serve`  
  （ポート 28765 で待機。AHKはここにPOSTして結果を受け取ります。）
- **単発モード（従来どおり）**: `python DokodemoLLM.py GPT` のようにモデル名を指定すると、クリップボードからペイロードを読んで1回だけ実行します。

## 動作のために必要な設定

1. **環境変数の設定**  
- **OpenAIのAPIキー**  
  OpenAIのAPIキーを取得し、以下の環境変数をセットしてください。  
  `OPENAI_API_KEY`  
  任意で `OPENAI_MODEL`（既定: `gpt-4o`）を設定すると別モデルを指定できます。
- **GoogleのAPIキー**  
  GeminiのAPIキーを取得し、以下の環境変数をセットしてください。  
  `GOOGLE_API_KEY`  
  任意で `GEMINI_MODEL`（既定: `gemini-2.5-flash`）を設定すると別モデルを指定できます。
- **DGX／ローカルLLM（Ctrl-Win-d用）**  
  ローカルやネットワーク上のLLMサーバー（例：NVIDIA DGX Spark上のvLLM）でOpenAI互換APIを提供している場合、`LOCALLLM_BASE_URL`、`LOCALLLM_MODEL`、必要なら`LOCALLLM_API_KEY`をセットしてください。詳しくは「ローカルLLM（DGX Spark）を使う場合（詳細）」を参照。
※使いたいものだけセットすればよく、複数使うときはそれぞれの環境変数をセットしてください。

2. DokodemoLLM.zipの解凍
DokodemoLLMのリポジトリの「リリース」からdokodemollm.zipをダウンロード。
適切なフォルダに展開してください。
解答したフォルダの中にあるDokodemoLLMahk.exeが入っています。
解凍フォルダのdistなどのフォルダとその中身は、DokodemoLLMahk.exeを実行するフォルダにそのまま置いてください。

3. **自動実行のための登録**  
WindowsのスタートアップメニューにDokodemoLLMahk.exeのショートカットを登録します。

## ショートカットの変更
ショートカット（`Win-Ctrl-o`、`Win-Ctrl-g`、`Ctrl-Win-d`）を変更したい場合は、ソースの DokodemoLLM.ahk を修正して使ってください。その場合は、AutoHotKeyをインストールして状態にしておく必要があります。
現状、以下のように設定されています。
- 「^#o::」は、Ctrl-Win-oで起動：OpenAIのGPT（modelは環境変数`OPENAI_MODEL`、既定 gpt-4o）
- 「^#g::」は、Ctrl-Win-gで起動：Gemini（modelは環境変数`GEMINI_MODEL`、既定 gemini-2.5-flash）
- 「^#d::」は、**Ctrl-Win-d**で起動：DGX／ローカルLLM（modelは環境変数`LOCALLLM_MODEL`で指定）

## ローカルLLM（DGX Spark）を使う場合（詳細）

DokodemoLLMはOpenAI互換APIをサポートしているため、NVIDIA DGX Sparkなどのマシン上で互換APIサーバーを起動すると、ローカルLLMとして利用できます。ここでは、vLLMをDGX Spark上でDockerコンテナとして動かす方法を例に説明します。

**ショートカット**: **Ctrl-Win-d** でDGX／ローカルLLMを呼び出します。

### 1. DGX Spark 側の設定（vLLM の起動）

- **前提**: NVIDIA DGX Spark（Ubuntu 22.04 LTS 推奨）、NVIDIAドライバ・CUDA、Docker および NVIDIA Container Toolkit がインストール済みであること。
- **vLLM コンテナの起動**: DGX SparkにSSHなどでログインし、次を実行します。
  ```bash
  docker run -d --gpus all -p 8000:8000 --shm-size=16g \
    --restart unless-stopped --name vllm-llama \
    nvcr.io/nvidia/vllm:26.01-py3 \
    vllm serve "nvidia/Llama-3.1-8B-Instruct-NVFP4" --host 0.0.0.0
  ```
- **起動確認**: `docker ps` および `docker logs -f vllm-llama` で確認。DGX上で `curl http://localhost:8000/v1/models` でモデル一覧（JSON）を取得。その `id` が環境変数 `LOCALLLM_MODEL` に設定する値です。
- **ファイアウォール**: Windowsから接続できない場合は、DGX側（SSHで）で `sudo ufw allow 8000` と `sudo ufw reload` を実行。

### 高性能モデル（70B）を使う場合

DGX Spark（128GB 統一メモリ）では、8B より高性能な **70B クラスの量子化モデル** も動作します。品質を上げたい場合は次のように切り替えてください。

1. **既存の 8B コンテナを止める**（同じポートで 70B を動かす場合）
   ```bash
   docker stop vllm-llama
   docker rm vllm-llama
   ```

2. **70B モデルで vLLM を起動する**  
   - **Llama 3.3 70B（推奨）** — 新しい世代で性能・指示追従が良いです。Blackwell 向け FP4 量子化:
     ```bash
     docker run -d --gpus all -p 8000:8000 --shm-size=32g \
       --restart unless-stopped --name vllm-llama \
       nvcr.io/nvidia/vllm:26.01-py3 \
       vllm serve "nvidia/Llama-3.3-70B-Instruct-FP4" --host 0.0.0.0
     ```
   - **Llama 3.1 70B** — 安定した選択肢。FP8 量子化（Blackwell/Hopper 両対応）:
     ```bash
     docker run -d --gpus all -p 8000:8000 --shm-size=32g \
       --restart unless-stopped --name vllm-llama \
       nvcr.io/nvidia/vllm:26.01-py3 \
       vllm serve "nvidia/Llama-3.1-70B-Instruct-FP8" --host 0.0.0.0
     ```

3. **Windows 側の環境変数を更新**  
   - `LOCALLLM_MODEL` を起動したモデル名に合わせて変更します。  
     - Llama 3.3 70B: `nvidia/Llama-3.3-70B-Instruct-FP4`  
     - Llama 3.1 70B: `nvidia/Llama-3.1-70B-Instruct-FP8`

4. **補足**
   - `--shm-size=32g` は 70B 用に 16g より大きくしています。メモリ不足になる場合は `--gpu-memory-utilization 0.85` などを vLLM のオプションで調整できます。
   - 初回はモデルダウンロードで時間がかかります。起動確認は `docker logs -f vllm-llama` で行えます。

5. **参考（70B モデルについて）**  
   Llama 3.3 70B Instruct FP4 は、Meta の 70B パラメータモデルを指令追従用にチューニングしたものを、NVIDIA が 4 ビット浮動小数点（FP4）に量子化したものです。DGX Spark の 128GB 統一メモリと Blackwell の FP4 対応を活かした構成で、70B を 1 台で動作させられます。性能の目安としては、OpenAI でいえば GPT-3.5 より上〜GPT-4 に近いクラスとされることが多く、GPT-4o ほどではありませんが多くのタスクで実用レベルです。

### 2. DokodemoLLM 側の設定（Windows PC）

- **環境変数**: `LOCALLLM_BASE_URL`（例: `http://192.168.50.203:8000/v1`）、`LOCALLLM_MODEL`（例: `nvidia/Llama-3.1-8B-Instruct-NVFP4`）、`LOCALLLM_API_KEY`（不要なら `EMPTY`）。
- **接続確認**: WindowsのPowerShellで `Test-NetConnection -ComputerName <DGXのIP> -Port 8000` および `curl.exe http://<DGXのIP>:8000/v1/models` で確認。

### その他

- **NVIDIA NIM** や **LM Studio** など、OpenAI互換APIを提供する他のサーバーも同様に `LOCALLLM_BASE_URL` 等で利用できます。
- `--host 0.0.0.0` で公開する場合は、ファイアウォールや必要に応じてvLLMのAPIキー認証などでセキュリティを確保してください。

## Macでの使用
1. **AutoHotKey以外のスニペットツールを用意**
適切なスニペットツールを使ってDokodemoLLM.pyを呼び出すようにスクリプトを作ってください。
したがって、Pythonの動作環境が必要となります。
スニペットツールからはプロンプトがDokodemoLLM.pyにクリップボードで渡され、DokodemoLLM.pyからはやはりクリップボード経由で結果がスニペットツールに戻されます。詳しくはソースコードをご覧ください。

## 免責事項

本ソフトウェアの利用によりユーザーが被った損害について、作者・貢献者は一切補償しません。個別の質問には基本的にお答えできません。ソースコードが公開されているため、AIに聞く、あるいはコードを自身で確認することを検討してください。とくにサーバー側の設定（ローカルLLM・vLLM・DGX Spark など）はユーザーの環境に依存するため、自身で解決してください。

