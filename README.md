# GLM-5.3-Flash on Google Colab

Strata-GLMでGLM-5.3-Flashを動かし、Colab内でチャットするためのノートブックです。**A100 80GB・RAM約167GiBで動作確認済み。** 修正コードとチャットUIを内蔵しています。

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/hamster-poodle/glm-5.3-flash-colab/blob/main/GLM_5_3_Flash_Strata_Colab_v3.ipynb)

## 使い方

1. 上の **Open in Colab** を押す。
2. 自分のGoogleアカウントで、ランタイムを **A100 GPU・高RAM** に設定する。
3. ノートブックの **1〜6** を順に実行する。
4. **8：チャットUI** を実行して会話する。7の速度測定は任意。

**必要条件：A100 80GB、RAM 150GiB以上、モデル146.05GiB＋作業用10GiB以上の空きディスク。** A100 40GBやT4向けの設定ではありません。ColabのGPU割当は保証されません。

モデル取得は約7〜8分、起動は約6〜9分を観測しました。初回はビルドも必要です。検証時の表示消費率は約6.77 CU/時。自分の利用枠・残りCUを確認してください。

詳細は **[実行手順・環境・トラブル対応（COLAB.md）](COLAB.md)** を参照してください。

## 動作確認の結果

| 項目 | 実測・設定 |
|---|---|
| モデル | 通常版 `unsloth/GLM-5.3-Flash-GGUF` / `UD-IQ4_XS` |
| 検証環境 | A100-SXM4-80GB / RAM167.1GiB / CUDA13.0 |
| GPUエキスパートキャッシュ | 66.36GiB |
| RAM常駐 | 67.46GiB（page-locked） |
| 生成速度 | 12.0 tok/s |
| 最初の出力 / 全体 | 7.33秒 / 34.45秒 |
| 入力 / 出力 | 61 / 328トークン、入力キャッシュ0、stop終了 |

2026-10-12の単発測定です。質問・回答長・割当で速度は変わります。RAM検出修正前は5.3 tok/sでした。expert skippingはオフ、コンテキスト設定は32Kです。

ビルド、RAM常駐、再起動、チャットの複数ターンを確認しました。共有版のコード検証と、固定ソースへの修正適用・再適用も確認しています。**第三者アカウントの新規ランタイムでの全工程実行、別GPU、32K最大長の負荷試験は未検証です。**

## 保存と終了

モデルはColabの一時ディスクへ取得します。Driveへのモデル退避は行いません。必要な回答は保存し、終了時は **「ランタイム → 接続解除してランタイムを削除」** で利用を終了してください。モデルも消えるため、新規ランタイムでは再取得します。

APIはColab内のループバック接続のみ。公開トンネルや外部の有料推論APIは使いません。ColabはGoogleのクラウドなので、ローカルPC内だけで完結する構成ではありません。

## 出典・ライセンス

- [Strata-GLM](https://github.com/isichan-ai/Strata-GLM)
- [モデル配布元](https://huggingface.co/unsloth/GLM-5.3-Flash-GGUF)
- [参考にしたQwen Colab手順](https://drive.google.com/file/d/1eop4zr2ofgRJDfdv6nZL4Lyo7vU_uPeU/view) — 本ノートブックの対象はGLMです。

エンジン由来コードは [MIT License](LICENSE)。モデル重みは含みません。モデルの利用条件は配布元を参照してください。
