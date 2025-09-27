# DokodemoLLM
It is a convenient tool that allows LLM to be called from any app.
どのアプリからもLLMを呼び出すことができる便利なツールです。

(c) 2025 Satoshi Endo  
https://x.com/hortense667
https://ascii.jp/serialarticles/1225476/

## Overview
This software allows you to call LLMs (OpenAI GPT, Google's Gemini) and input the results in most Windows software where text input is required.

## Usage Instructions

1. **Execute DokodemoLLMahk.exe**  
   Obtain an API key from OpenAI or Gemini and set it as an environment variable. Then, simply unzip the distribution package and execute DokodemoLLMahk.exe. An icon will appear in the system tray.
   Please download the package from the next release: https://github.com/hortense667/DokodemoLLM/releases/tag/V1.0.0

2. **How to Call LLM**  
   2-1. Select Text in Input Area  
   First, select the text you want to process in the input or editing area of applications like Gmail, Word, or text editors.

   2-2. Input Prompt  
   Use `Win-Ctrl-o` to call OpenAI GPT or `Win-Ctrl-g` for Gemini. The UI consists of a dropdown list and a simple editor. For the first prompt, enter it in the simple editor and press "OK". You can select previously entered prompts from the dropdown list. They are listed in order of the most recently used, so navigate with the arrow keys. You can also display a list by clicking the "v" on the right. The selected prompt will be displayed in the simple editor window, allowing you to edit it if needed. Once your prompt is set, click "OK". Prompt history is saved as "prompt_history.txt" in the folder where DokodemoGPT02ahk.exe is executed, up to a maximum of 100 entries. Examples include simple prompts like "Rewrite for readability", "Summarize", "Translate to English", "Check for typos", or more complex prompts with line breaks. 
   Note: If you append "/w" at the end of a prompt, it will perform a web search and use the first 1000 characters from the top 3 sites as a reference.

3. **Confirm Content**  
   After a few seconds or up to several tens of seconds, a window will appear asking, "Is this okay?"  
   - "Yes": Replaces with the result  
   - "No": No changes made  
   - "Cancel": Appends the result to the original text.

## Necessary Settings for Operation

1. **Set Environment Variables**  
   - **OpenAI API Key**  
     Obtain an OpenAI API key and set the following environment variable:  
     `OPENAI_API_KEY`
   - **Google API Key**  
     Obtain a Gemini API key and set the following environment variable:  
     `GEMINI_API_KEY`
   Note: You can set only the one you want to use, or both if you want to use both.

2. Unzip DokodemoLLM.zip  
   Download dokodemollm.zip from the "Releases" section of the DokodemoLLM repository. Unzip it to an appropriate folder. DokodemoLLMahk.exe is included in the extracted folder. Leave the dist folder and its contents in the same folder where you execute DokodemoLLMahk.exe.

3. **Register for Auto Execution**  
   Register a shortcut to DokodemoLLMahk.exe in the Windows startup menu.

## Changing Shortcuts
If you want to change the shortcuts (`Win-Ctrl-o` or `Win-Ctrl-g`), modify DokodemoGpt02ahk.ahk in the source folder. In this case, you need to have AutoHotKey installed and running. Currently, the settings are as follows:
- "^#o::" launches with Ctrl-Win-o: OpenAI GPT (model="gpt-4o")
- "^#g::" launches with Ctrl-Win-g: Gemini (model="gemini-2.5-flash")

## Usage on Mac
1. **Prepare a Snippet Tool Other than AutoHotKey**  
   Use an appropriate snippet tool to create a script that calls DokodemoLLM.py. Therefore, a Python environment is required. The snippet tool passes the prompt to DokodemoLLM.py via clipboard, and the result is returned to the snippet tool via clipboard as well. Please see the source code for details.

## 概要
Windowsのほとんどのソフトウェアのテキストを入力するシーンでLLM（OpenAI GPT、GoogleのGemini）を呼び出して結果を入力できるソフトウェアです。

## 使い方の手順

1. **DokodemoLLMahk.exeの実行**  
OpenAI、たまは、GeminiのAPIキーを取得して環境変数に設定してください。あとは、配布パッケージのzipを解凍してDokodemoLLMahk.exeを実行するだけ。トレイにアイコンが現れます。
パッケージは、次のリリースからダウンロードしてください。https://github.com/hortense667/DokodemoLLM/releases/tag/V1.0.0

3. **LLMの呼び出し方**  
2-1. テキスト入力エリアで範囲選択  
まず、Gmail、Word、テキストエディタなどの入力・編集画面で処理対象にしたい部分を範囲選択します。

2-2. プロンプトの入力  
`Win-Ctrl-o`でOpenAIのGPT、`Win-Ctrl-g`でGeminiが呼び出されます。
UIは、ドロップダウンリストと簡易エディタからなっています。
初めて入力するプロンプトは簡易エディタを入力したあと「OK」を押してください。
ドロップダウンリストから過去に入力したプロンプトを選ぶことができます。最後に使ったものから順に並んでいるのでカーソキーで選びましょう。また、右側の「v」から一覧表示することもできます。
選んだプロンプトが、簡易エディタの窓に表示されるので、それを編集して使うこともできます。
プロンプトが決まったら「OK」をクリックします。
なお、過去のプロンプトの履歴は最大100件までDokodemoGPT02ahk.exeを実行したフォルダ上に「prompt_history.txt」というファイルに作成されます。
例：「読みやすく書き換えて」「要約して」「英訳して」「誤字・脱字をチェック」など簡単なプロンプトから改行を含んだ複雑なプロンプトまで入力できます。
※「どんな人？/w」などと最後に「/w」をつけるとWeb検索して最初の3つのサイトの冒頭1000文字を参考に答えます。

3. **内容確認**  
数秒から数十秒が経過すると「これでよいですか？」というウィンドウが表示されます。  
- 「はい」：結果に置き換えられる  
- 「いいえ」：変更なし  
- 「キャンセル」：元の文に続いて結果が入力されます。

## 動作のために必要な設定

1. **環境変数の設定**  
- **OpenAIのAPIキー**  
  OpenAIのAPIキーを取得し、以下の環境変数をセットしてください。  
  `OPENAI_API_KEY`
- **GoogleのAPIキー**  
  GeminiのAPIキーを取得し、以下の環境変数をセットしてください。  
  `GEMINI_API_KEY`
※どちらか一方、使いたいほうだけでセットしてもよいし、両方使いたいときは両方セットしてください。

2. DokodemoLLM.zipの解凍
DokodemoLLMのリポジトリの「リリース」からdokodemollm.zipをダウンロード。
適切なフォルダに展開してください。
解答したフォルダの中にあるDokodemoLLMahk.exeが入っています。
解凍フォルダのdistなどのフォルダとその中身は、DokodemoLLMahk.exeを実行するフォルダにそのまま置いてください。

3. **自動実行のための登録**  
WindowsのスタートアップメニューにDokodemoLLMahk.exeのショートカットを登録します。

## ショートカットの変更
ショートカット（`Win-Ctrl-o`や`Win-Ctrl-g`）を変更したい場合は、sourceフォルダにあるDokodemoGpt02ahk.ahkを修正して使ってください。その場合は、AutoHotKeyをインストールして状態にしておく必要があります。
現状、以下のように設定されています。
- 「^#o::」は、Ctrl-Win-oで起動：OpenAIのGPT（model="gpt-4o"）
- 「^#g::」は、Ctrl-Win-gで起動：Gemini（model="gemini-2.5-flash"）

## Macでの使用
DokodemoLLM4Macをご検討ください。
Pythonの動作環境が必要となります。

