# 🗣️ 音声からの身長推定ツール (F0 & VTLモデル)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yakimisan/Voice-Height-Analyzer/blob/main/声から二種類の方法で身長を推定するコード.ipynb)
これは、アップロードされた音声ファイルから「声の高さ(F0)」と「声の響き(VTL)」を分析し、2つの異なる音響学モデルに基づいて身長を推定するGoogle Colabツールです。

## 🚀 使い方 (How to Use)

1.  上の **"Open in Colab"** バッジをクリックします。
2.  ノートブックがGoogle Colabで開きます。
3.  一番上の説明文を読み、**実行セル (▶️)** をクリックして実行します。
4.  `gender:` のドロップダウンで性別を選択します。
5.  `[ファイルを選択]` ボタンで、分析したい音声ファイル（.wav, .mp3など）をアップロードします。
6.  自動的に分析が実行され、結果が出力されます。

---

## 🔬 2つの推定モデルについて

本ツールは、あえて2つの異なるアプローチを実装し、その結果を比較できるようにしています。

### 1. モデル1: F0 (声の高さ) モデル
F0（基本周波数＝声の高さ）と身長には、一般的に負の相関（背が高い人ほど声帯が長く、F0が低くなる傾向）があることが知られています。

このモデルは、その統計的相関（Hatano et al., 2012）に基づき、「声の高さ」から身長を推定します。

* **長所**: 概念が直感的でわかりやすい。
* **短所**: F0は「中性的な声」や「低い声」など、**発声の癖や意図によって大きく変動**するため、物理的な身長との相関が弱まることがあります。

### 2. モデル2: VTL (声道長・響き) モデル
VTL（声道長）は、声帯から唇までの「音の共鳴管」の長さです。このVTLは身長と強い物理的相関があります。

F0（声帯の振動）とは異なり、VTL（管の長さ）は発声の癖（ソフトウェア）では変えにくいため、より安定した**物理的な特徴（ハードウェア）**と言えます。

このモデルは、以下の2段階で推定を行います。
1.  **音声 $\rightarrow$ フォルマント $\rightarrow$ VTL推定**:
    声の「響き」（フォルマント周波数）を分析し、その響きを生み出している管の長さ(VTL)を逆算します。
2.  **VTL $\rightarrow$ 身長推定**:
    推定されたVTLと身長の統計的な関係性（Fitch & Giedd, 1999など）に基づき、最終的な身長を推定します。

---

## ⚠️ 免責事項 (Disclaimer)

* [日本語] 本ツールは、音響学の理論に基づく統計的な推定であり、その精度を保証するものではありません。発話内容、マイクの品質、環境ノイズ、発声の癖によって結果は大きく変動します。
* [English] This tool is a statistical estimation based on acoustic theory, and its accuracy is not guaranteed. Results may vary significantly depending on speech content, microphone quality, environmental noise, and vocal habits.

* [日本語] 本ツールの推定結果は、あくまで音響学的な参考値として、エンターテイメントの範囲でお楽しみください。 正確な身長を示すものではありません。
* [English] The estimation results of this tool should be enjoyed within the scope of entertainment as purely acoustic reference values. They do not indicate exact height.

* [日本語] 本ツールの利用は、すべて利用者ご自身の責任において行ってください。本ツールの使用、またはその結果の利用によって生じたいかなる損害（データの損失、法的な紛争を含む）についても、製作者(yakimi)は一切の責任を負いません。
* [English] Use of this tool is entirely at your own risk. The author (yakimi) assumes no responsibility for any damages (including data loss or legal disputes) arising from the use of this tool or its results.

## 📜 ライセンスと利用上の禁止事項 (License & Prohibitions)

[日本語]
本ソフトウェアは、製作者（やきみ）が定める独自の利用許諾契約書（カスタムライセンス）のもとで提供されます。
ご利用の前に、必ず以下のライセンス全文をお読みください。

[English]
This software is provided under a custom Software License Agreement defined by the author (やきみ).
Please read the full license text before using the software.

➡️ **[LICENSE.txt (利用許諾契約書 全文 / Full License Agreement)](LICENSE.txt)**

[日本語]
本ソフトウェアを利用した時点で、ライセンス全文に同意したものとみなされます。
特に、本ライセンスの第2条（制限事項）に基づき、**以下の行為は固く禁止されています。**

1.  **許可なく第三者（自分以外）の音声を分析し、その推定結果をインターネット上で公開する行為。**
2.  **個人の特定、他者の名誉毀損、またはその他の違法な目的・犯罪行為に利用すること。**

[English]
By using this software, you agree to be bound by all terms of the license.
In particular, under Article 2 (Restrictions) of this license, **the following acts are strictly prohibited:**

1.  **Analyzing the voice of a third party (anyone other than yourself) without permission and publishing the estimated results online.**
2.  **Using the tool for personal identification, defamation, or any other illegal or criminal purpose.**

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
## 📚 参考文献 (References)

このツールで採用している理論は、以下の研究に基づいています。

#### 1. F0と身長の相関
* **Hatano, H., Kitamura, T., Takemoto, H., Mokhtari, P., Honda, K., & Masaki, S. (2012).** "Correlation between vocal tract length, body height, formant frequencies, and pitch frequency for the five Japanese vowels uttered by fifteen male speakers". *Proceedings of Interspeech 2012*.

#### 2. VTL（フォルマント・声道長）と身長の相関
* **Fant, G. (1960).** *Acoustic theory of speech production*. Mouton.
* **Stevens, K. N. (1998).** *Acoustic phonetics*. MIT press.
* **Fitch, W. T., & Giedd, J. (1999).** "Morphology and development of the human vocal tract: A study using magnetic resonance imaging". *Journal of the Acoustical Society of America*, 106(3), 1511-1522.

## 👤 製作者 (Author)

* **yakimi**


