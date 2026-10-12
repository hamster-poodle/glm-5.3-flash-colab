# GLM-5.3-FlashをGoogle Colabで使う

Strata-GLMで動かす、画像・文書・URL入力に対応したチャットです。**通常版（Unsloth）／Abliterated版（Huihui）** を選べます。

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hamster-poodle/glm-5.3-flash-colab/blob/main/GLM_5_3_Flash_Strata_Colab_v3.ipynb)

## 始め方

1. **Open in Colab** を押し、自分のGoogleアカウントでログイン。
2. 「ランタイム → ランタイムのタイプを変更」で **A100・高RAM** を選択。
3. モデルを選び、**「チャットを起動」の▶** を押す。
4. 準備が終わったら質問を入力。ファイルは選ぶだけで添付され、URLは「URLを読み込む」で追加できます。

**必要環境：A100 80GB・RAM 150GiB以上・モデル約157GB＋作業領域。** A100を利用できる有料利用枠が必要です。[Google AI Pro](https://one.google.com/about/google-ai-plans/)で検証しましたが、契約してもGPU割当は保証されません。[プラン・対象条件の詳細](COLAB.md#事前準備プランを選ぶ)を確認してください。

初回はモデル取得約7〜8分、起動約6〜9分に加え、ビルド時間がかかります。所要時間は環境で変わり、稼働中はColabの利用枠を消費します。

## できること

- テキストでの会話、画像の説明・文字読取、PDFや文書への質問、公開URLの読取。
- 会話をJSONで保存・復元、Markdownで保存。
- 通常版／Huihui Abliterated版の選択（どちらもUD-IQ4_XS）。切替は会話を保存してランタイムを削除し、選び直して再取得します。

添付は1ファイル10MiB、1送信につき画像2枚・資料本文約16,000文字まで。画像は長辺768pxへ縮小します。Web検索・ログインサイト・音声・動画には対応していません。

## 保存と終了

必要な会話は **「履歴JSONを保存」**。終了は **「接続解除してランタイムを削除」** を押してください。未保存の会話・添付とモデルは失われ、次回はモデルを再取得します。

処理はGoogle Colab内で実行します。会話や添付がこのGitHubへ自動公開されることはありません。外部の有料推論API・公開トンネルは使いません。

## 検証・出典

異常な計算結果を検知し、内部状態のリセットと最大1回の再試行を行うGLM専用対策を追加しました。失敗時も質問・添付を保持します。[v0.1.43情報の採用方針と検証](COLAB.md#v0143情報の採用方針)をご覧ください。

**A100 80GB・RAM167.1GiBでテキスト／画像／文書＋URLの回答を確認済み。** Huihui版は新規ランタイムで取得・ビルドから検証しました（2026-10-12）。長時間安定性・両モデルの品質比較は未検証です。

[詳細・実測・トラブル対応](COLAB.md) · [Strata-GLM](https://github.com/isichan-ai/Strata-GLM) · [通常版モデル](https://huggingface.co/unsloth/GLM-5.3-Flash-GGUF) · [Huihuiモデル](https://huggingface.co/huihui-ai/Huihui-GLM-5.3-Flash-abliterated-GGUF)

エンジン由来コードは [MIT License](LICENSE)。モデル重みは含みません。モデルの利用条件は各配布元を参照してください。
