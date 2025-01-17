﻿# 簡単プロンプトアニメ

[AnimateDiff prompt travel](https://github.com/s9roll7/animatediff-cli-prompt-travel) を使って、ローカル PC で簡単に動画を生成する環境です。  
**[[ 概要 ](https://twitter.com/Zuntan03/status/1704807854384066714) ] [[ Colab版 ](https://twitter.com/Zuntan03/status/1703674198101803268)]**  
[![title](./doc/img/title.webp)](https://yyy.wpx.jp/m/202309/KuronekoAkiba.mp4)

- プロンプトだけで FullHD のスムーズな長尺動画を生成
- セットアップ・2段アップスケール・フレームレート補間などが自動
- [AnimateDiff prompt travel](https://github.com/s9roll7/animatediff-cli-prompt-travel) の生成設定ファイルを流用可能

## 作例

- 9/24: [モデルへの VAE 組み込み有無比較](https://twitter.com/Zuntan03/status/1705779826056147188) の [きれいな動画](https://yyy.wpx.jp/m/202309/ModelVae-crf26.mp4)
- 9/23: [motion-moduleのmm_sd_v15_v2とmm-Stabilized_high比較](https://twitter.com/Zuntan03/status/1705537060491432132) [FullHD 超え動画](https://yyy.wpx.jp/m/202309/V152HighGrid.mp4)
- 9/21: FullHD 相当 [KuronekoAkiba](https://yyy.wpx.jp/m/202309/KuronekoAkiba.mp4)
- 9/18: [nadenadesitai_v10](https://yyy.wpx.jp/m/202309/nadenadesitai_v10.mp4), [xxmix9realistic_v40](https://yyy.wpx.jp/m/202309/xxmix9realistic_v40.mp4), [onigiriMix_v10](https://yyy.wpx.jp/m/202309/onigiriMix_v10.mp4), [mistoonAnime_v20](https://yyy.wpx.jp/m/202309/mistoonAnime_v20.mp4)
- 利用者のつぶやき（通知があったもののみ）
	- [1](https://twitter.com/llrinnell/status/1703711755128779226),
[2](https://twitter.com/ai_gene_fumo7/status/1704116905299382547),
[3](https://twitter.com/moshimur/status/1704322583095812332),
[4](https://twitter.com/mouriAIart/status/1704986700358013430),
[5](https://twitter.com/katarina7410/status/1705152174471463009),
[6](https://twitter.com/PhotogenicWeekE/status/1705175475176530146),
[7](https://twitter.com/safa_dayo/status/1705183157920616482),
[8](https://twitter.com/hina_chocoboo13/status/1705213931466485813),
[9](https://twitter.com/cigmatari/status/1705225865356009612),
[10](https://twitter.com/keythpiece/status/1705605784091193717),
[11](https://twitter.com/TakaWeekendProg/status/1705745532424233372),
[12](https://twitter.com/llrinnell/status/1705898369586212877)

## 主な更新履歴

- 2024/09/24
	- **今回の更新では `Update.bat` を 2回！実行してください（`Update.bat` を更新したため）。**
	- [AnimateDiff prompt travel](https://github.com/s9roll7/animatediff-cli-prompt-travel) の更新に対応しました。
		- AnimateDiff 用にモデルを修正する `FixCheckpoint.bat` を追加しました。<br>
		が、手元で利用しているモデルは修正不要でした。
	- 生成した動画のサイズを低減する `Mp4Crf(26|32|38)` を追加しました。
	- 生成した動画から X(Twitter) 投稿用の動画を生成する `XMp4*.bat` を追加しました。
- 2023/09/23
	- 生成する動画のデフォルトの FPS を、様々なサービスとの互換性の観点から 40FPS にしました。
		- 生成設定ファイル名に `-D3` を付け足すと、以前と同様に 80FPS になります。
		- FPS 指定の詳細は [ファイル名オプション一覧](#ファイル名オプション一覧) や `FpsX4.bat` の説明を参照してください。
	- 生成した mp4 ファイル名に、日時のプレフィックスを追加するようにしました。
		- 同一シードで生成しても、mp4 ファイルを上書きしなくなります。
- 2023/09/22
	- motion-module に mm-Stabilized_high.pth と mm-Stabilized_mid.pth を追加しました。
		- `Update.bat` を実行するとダウンロードします。
	- 同一シードで同じフォルダに再出力した際に、正しくフレーム補間されない不具合を修正しました。
		- インストール済みの方は `Update.bat` を実行してください。
	- インストーラーで `C:\Windows\System32` にパスが通っていない場合にエラー扱いにしました。
- 2023/09/21
	- 公開

## 動作環境

- Windows 10 以降（Windows Update済み）の PC で、Windows/System32 にパスが通っている
- 最近の NVIDIA Geforce RTX **VRAM 8BG 以上**
- パスを通した [Python 3.10.6](https://www.python.org/ftp/python/3.10.6/python-3.10.6-amd64.exe) と [Git for Windows](https://gitforwindows.org/)

## セットアップ

1. 動作環境の [Python 3.10.6](https://www.python.org/ftp/python/3.10.6/python-3.10.6-amd64.exe) を導入していない場合は、[Python のインストール](https://github.com/Zuntan03/SdWebUiTutorial/blob/main/_/doc/SdWebUiInstall/SdWebUiInstall.md#python-%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB) をします。
2. 動作環境の [Git for Windows](https://gitforwindows.org/) を導入していない場合は、[Git for Windows のインストール](https://github.com/Zuntan03/SdWebUiTutorial/blob/main/_/doc/SdWebUiInstall/SdWebUiInstall.md#git-for-windows-%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB) をします。
2. [Civitai](https://civitai.com) がダウンしていないか確認します。
3. [Setup-EasyPromptAnime.bat](https://github.com/Zuntan03/EasyPromptAnime/raw/main/src/Setup-EasyPromptAnime.bat) を **右クリックから「名前をつけてリンク先を保存…」** でインストール先のフォルダ（英数字のみの浅いパス）にダウンロードして実行します。
	- **「WindowsによってPCが保護されました」と表示されたら、「詳細表示」から「実行」します。**  
4. インストールが終わると、Google Colabでプロンプト編集用の「[簡単プロンプトアニメエディタ](https://colab.research.google.com/drive/1XeVRMmw-dyALMacKU-_Xj2nMboZL_TM3)」が立ち上がります。

### セットアップ FAQ

- 動画の生成が一晩経っても終わらない、サンプル（`sample/UpscaleGacha.bat`、RTX 3060 で約 15分）の生成に長い時間が掛かる
	- [AI 画像生成の VRAM オフロード問題](https://www.google.com/search?q=%E7%94%BB%E5%83%8F%E7%94%9F%E6%88%90+VRAM%E3%82%AA%E3%83%95%E3%83%AD%E3%83%BC%E3%83%89%E5%95%8F%E9%A1%8C)を踏んでいる可能性がありますので、グラフィックスドライバのバージョンを確認してください。
- セットアップでダウンロードされるモデルで動画を正常に生成できない
	- モデルのダウンロードに失敗している場合がありますので、`animatediff-cli-prompt-travel/data/models/sd/` にある該当ファイルを削除し、`src/Setup.bat` で再ダウンロードしてください。

## 更新方法

簡単プロンプトアニメを更新するには、`Update.bat` を実行します。

## つかい方

12秒のアニメをとりあえず生成してみたい方は、`sample/UpscaleGacha.bat` を実行してみてください(RTX 3060 で約 15分)。

1. `OpenClabEditor.bat` で「[簡単プロンプトアニメエディタ](https://colab.research.google.com/drive/1XeVRMmw-dyALMacKU-_Xj2nMboZL_TM3)」を開きます。
2. ひとつめの`▶`を押してプロンプト入力欄を表示し、プロンプトやパラメータを編集して、ふたつめの`▶`を押すと動画生成用の生成設定ファイル (*.json) をダウンロードします。
3. 生成設定ファイルをインストール先([Setup-EasyPromptAnime.bat](https://github.com/Zuntan03/EasyPromptAnime/raw/main/src/Setup-EasyPromptAnime.bat) を実行したフォルダ)にある `Generate.bat` にドラッグ＆ドロップすると、生成設定ファイルの場所に動画を生成します。
	- 生成した動画とフレームレート補間した動画と再エンコードした動画を生成します。

## FAQ

### 効率的にシードガチャをしたい

- アップスケールを無効にしたり、アップスケールのサイズを下げたりすることで効率的にシードガチャができます。
- プロンプトをざっくり詰める段階なら、最初の生成解像度を下げたり、短時間にして先頭付近のキーフレームで検証するのも手です。

### ガチャ結果動画のシード値を知りたい

- mp4 ファイル名先頭の `日時(MMDD_HHMM_SS)-数値` の `数値` 部分がシードです。
- `animatediff-cli-prompt-travel/(output|upscaled|refine)/` 以下にある `prompt.json` でも確認できます。

### 真っ黒の動画が生成されてしまう

以下のいずれかの手順で、改善するかもしれません。

1. `FixCheckpoint.bat` でモデルを修正します。モデルが書き換わる可能性があります。
2. 生成設定ファイルのファイル名に `-V` を付け足します（改善報告あり）。
3. [モデルの VAE を差し替え](#stable-diffusion-model-toolkit-によるモデルへの-vae-埋め込み方法)ます。
4. 生成設定ファイルのファイル名に `-X` を付け足します（未検証、`-V`, `-v`, `-x` との併用も）。
5. 別のモデルを使います。

### 「[簡単プロンプトアニメエディタ](https://colab.research.google.com/drive/1XeVRMmw-dyALMacKU-_Xj2nMboZL_TM3)」の初期値や選択肢を変えたい
- Colab のメニュー `ファイル - ドライブにコピーを保存` して、一番下の `コードを表示` から該当部分を編集します。

### モデルを追加したい

1. `FixCheckpoint.bat` でモデルを修正します。モデルが書き換わる可能性があります。
2. `animatediff-cli-prompt-travel/data/models/sd/` にモデルを置きます。
	- **[！注意！] [stable-diffusion-model-toolkit](https://github.com/arenasys/stable-diffusion-webui-model-toolkit) などで、[モデルに VAE を埋め込んでください](#stable-diffusion-model-toolkit-によるモデルへの-vae-埋め込み方法)。** <br>
	モデルに VAE を埋め込まないと、[このようになる](https://twitter.com/Zuntan03/status/1705779826056147188) 場合があります。
3. Colab ソースの `model_name = "nadenadesitai_v10" # @param [...]` の `...` を書き換えます。

AnimateDiff とモデルに相性があり、[黒画像になる](#真っ黒の動画が生成されてしまう)、あまりアニメーションしない、といった場合があります。

#### [stable-diffusion-model-toolkit](https://github.com/arenasys/stable-diffusion-webui-model-toolkit) によるモデルへの VAE 埋め込み方法

1. [Stable Diffusion web UI](https://github.com/AUTOMATIC1111/stable-diffusion-webui) に [stable-diffusion-model-toolkit](https://github.com/arenasys/stable-diffusion-webui-model-toolkit) をインストールします。
2. Stable Diffusion web UI の `Toolkit` タブで `リフレッシュ` してから `入力` で VAE を埋め込むモデルを選択して `読み込み` ます。
3. `高度な設定`	に移り、`Component - Class` から `VAE-v1` を選択します。
4. `実行 - ファイル` で埋め込む VAE を選択して `Import` します。
5. `名前` で VAE を埋め込んだモデルのファイル名を指定して `保存` で、モデルフォルダに VAE を埋め込んだモデルが保存されます。
6. `animatediff-cli-prompt-travel/data/models/sd/` に VAE を埋め込んだモデルを移動します。

### モーションモジュールを追加したい
1. `animatediff-cli-prompt-travel/data/models/motion-module/` にモーションモジュールを置きます。
2. Colab ソースの `motion_module = "mm_sd_v15_v2.ckpt" # @param [...]` の `...` を書き換えます。

### LoRA を使いたい
- `animatediff-cli-prompt-travel/data/lora/` に LoRA を置きます。
	- 使える LoRA は通常の LierLa 形式で、C3Lier(Locon) 以降は使えないっぽいです。
- LoRA の読み込みは、プロンプトエディタの `L:` で始める行で指定します。

### TI を使いたい
- `animatediff-cli-prompt-travel/data/embeddings/` に TI を置きます。

### ControlNet を使いたい
- [AnimateDiff prompt travel](https://github.com/s9roll7/animatediff-cli-prompt-travel) がそのまま動作していますので、生成設定ファイルを手書きすれば使えます。
- そのうち対応するかも？

### Widlcard を使いたい

- `animatediff-cli-prompt-travel/wildcards/` にワイルドカードを置きます。

### Refine がメモリ不足で落ちる
- context を半分にしていますが、落ちますね。
- 初回のアップスケールで解像度を抑えつつ Refine を使用、とかもできましたが、重い印象でした。

### ストレージ容量が足りない
- まずは [WizTree](https://forest.watch.impress.co.jp/library/software/wiztree/) で状況を確認してください。それでもストレージ容量が足りなかったら、買ってください。

### Colabで編集する意味ある？
- ありません。「[Colab版簡単プロンプトアニメ](https://colab.research.google.com/drive/1QVxBjAamxOIAAlSohQklZltRPx8WsxEN)」のコードを流用しただけなので、利用者が多そうだったらローカルエディタを用意する、かも。

## 各ツールの説明

- `OpenColabEditor.bat`
	- 「[簡単プロンプトアニメエディタ](https://colab.research.google.com/drive/1XeVRMmw-dyALMacKU-_Xj2nMboZL_TM3)」を開きます。
- `Generate.bat`
	- 生成設定ファイルをドラッグ＆ドロップすると、動画を生成します。
- `GenerateForever.bat`
	- 生成設定ファイルをドラッグ＆ドロップすると、動画を生成し続けます。終了時は `Ctrl+C` で止めてください。
- `Update.bat`
	- 簡単プロンプトアニメと [AnimateDiff prompt travel](https://github.com/s9roll7/animatediff-cli-prompt-travel) を更新します。
- `FixCheckpoint.bat`
	- モデルをドラッグ＆ドロップすると、モデルに問題があれば AnimateDiff 用に修正します。モデルが書き換わったかどうかは更新日時で確認してください。
- `FpsX4.bat`
	- mp4 をドラッグ＆ドロップすると、[RIFE](https://github.com/megvii-research/ECCV2022-RIFE/tree/main) で FPS を4倍にします。サイズが大きくなるので再エンコード版も生成します。
		- 第 2 引数に RIFE による中割りの分割回数（FPSの倍増を何回実施するかの）を指定できます。FPSが 1 なら 2倍、2 なら 4倍、3 なら 8倍、4 なら 16倍になります。未指定や 0 なら 2 になります。
		- 第 3 引数に RIFE の分割後の FPS を指定できます。 **この FPS 指定では画像の枚数を変更せずに FPS を適用しますので、アニメーションの速度と長さが変わります。** 1秒の 10FPS の動画を RIFE で 4倍にして 40枚の画像がある状態で、第三引数で 60FPS を指定すると、アニメーションが早くなり 0.66秒で再生が終わります。逆に 8倍で80枚にして 60FPS を指定した場合は、ゆっくり再生されて 1.33秒で再生が終わります。0 なら未指定です。
		- 第 4 引数で ffmpeg による再エンコード時の FPS を指定できます。再生速度や動画の長さは変わりません。0 なら未指定です。
		- 第 5 引数で ffmpeg による再エンコード時の crf を指定できます。未指定や 0 なら 20 になります。
- `Frames2Mp4.bat`
	- Tile アップスケールは mp4 を生成しませんが、`animatediff-cli-prompt-travel\upscaled` にある連番 png が入っているフォルダをドラッグ＆ドロップすると、mp4 を生成します。
- `DeleteOutput.bat`
	- ストレージ容量を消費しがちな `animatediff-cli-prompt-travel/` の `output/*/`, `upscaled/*/`, `refine/*/` を削除します。
- `Mp4Crf26.bat`, `Mp4Crf32.bat`, `Mp4Crf38.bat`
	- mp4 をドラッグ＆ドロップすると、Crf26 で 1/2、Crf32 で 1/4、Crf38 で 1/8 ぐらいのサイズの mp4 に変換します。
- `XMp4.bat`, `XMp4W1920.bat`, `XMp4W1200.bat`, `XMp4H1900.bat`, `XMp4H1200.bat`
	- mp4 をドラッグ＆ドロップすると X(Twitter) アップロード用の動画(40FPS, 25Mbps)を生成します。
		- [Xで動画を共有および視聴する方法](https://help.twitter.com/ja/using-x/x-videos#:~:text=%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%81%8B%E3%82%89%E3%82%A2%E3%83%83%E3%83%97%E3%83%AD%E3%83%BC%E3%83%89%E3%81%A7%E3%81%8D%E3%82%8B%E5%8B%95%E7%94%BB%E3%81%AE%E8%A7%A3%E5%83%8F%E5%BA%A6%E3%81%A8%E7%B8%A6%E6%A8%AA%E6%AF%94%E3%82%92%E6%95%99%E3%81%88%E3%81%A6%E3%81%8F%E3%81%A0%E3%81%95%E3%81%84%E3%80%82)
		- 動画の大きさが W1920 x H1200 か W1200 x H1900 に収まらない場合は、`XMp4W1920.bat`, `XMp4W1200.bat`, `XMp4H1900.bat`, `XMp4H1200.bat` を使用して、W1920 x H1200 か W1200 x H1900 に収まるように縮小します。
		- mp4 ファイル名の末尾が `*-D2e.mp4` な再エンコード後の mp4 でなく、`*-D2.mp4` な再エンコード前の mp4 から生成したほうが、品質が高くなります。

## [AnimateDiff prompt travel](https://github.com/s9roll7/animatediff-cli-prompt-travel) 利用者向け情報

既存のコンフィグファイルのファイル名にオプションを指定することで、`Generate.bat` が色々やってくれます。  
ハイフン(`-`)は引数の指定に使用するため、ファイル名には使えません。

例） `Config-L30-C16-W448-H544-T1088-T1632.json` を `Generate.bat` にドロップ
1. `animediff generate -L 30 -C 16 -W 448 -H544`
2. `animediff tile-upscale -H 1088` から ffmpeg で mp4 生成
	- `-R` なら `animediff refine -C (context / 2)`
3. `animediff tile-upscale -H 1632` から ffmpeg で mp4 生成
4. [RIFE](https://github.com/megvii-research/ECCV2022-RIFE/tree/main) でフレーム補間

### ファイル名オプション一覧

|キー|デフォルト値|説明|
|---:|---:|----|
|L|30|動画のフレーム総数を指定します。|
|C|16|AnimeDiffのコンテキスト長を指定します。|
|W|384|動画の幅を指定します。|
|H|512|動画の高さを指定します。|
|T|-|Tile アップスケール後の動画の高さを指定します。2回指定できます。|
|R|-|Refine アップスケール後の動画の高さを指定します。2回指定できます。|
|D|2|RIFE による中割りの分割回数を指定します。`FpsX4.bat` の第 2 引数説明参照。|
|I|0|RIFE による中割り後の FPS を指定します。`FpsX4.bat` の第 3 引数説明参照。|
|F|0|ffmpeg で mp4 に変換する際の FPS を指定します。`FpsX4.bat` の第 4 引数説明参照。|
|M|20|ffmpeg で mp4 に変換する際の crf を指定します。`FpsX4.bat` の第 5 引数説明参照。|
|U|10|Tile アップスケール後の画像を MP4 にする際のFPSを指定します。|
|v|-|動画の生成で half-vae を有効にします。|
|V|-|動画のアップスケールで half-vae を有効にします。|
|x|-|動画の生成で xFormers を有効にします。|
|X|-|動画のアップスケールで xFormers を有効にします。|

## 参照

- [AnimateDiff prompt travel](https://github.com/s9roll7/animatediff-cli-prompt-travel) 
- [Codex FFmpeg](https://github.com/GyanD/codexffmpeg)
- [Real-Time Intermediate Flow Estimation for Video Frame Interpolation](https://github.com/megvii-research/ECCV2022-RIFE)

# ライセンス

このリポジトリのスクリプトやドキュメントは、[MIT License](./LICENSE.txt)です。

This software is released under the MIT License, see [LICENSE.txt](./LICENSE.txt).
