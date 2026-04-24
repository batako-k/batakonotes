# zkp-notes
My study notes on Zero-Knowledge Proofs

## Topics
- What is ZKP
- Add topics section

# Zero-Knowledge Proof (ZKP)

## 1. Completeness（完全性）

もし $x \in L$ なら、正しい証明者 $P$ に対して検証者 $V$ は受理する：

$$
x \in L \Rightarrow \Pr[V \ accepts] \approx 1
$$

---

## 2. Soundness（健全性）

もし $x \notin L$ なら、不正な証明者はほぼ騙せない：

$$
x \notin L \Rightarrow \Pr[V \ accepts] \approx 0
$$

---

## 3. Zero-Knowledge（ゼロ知識性）

検証者が見る情報は、シミュレーターでも生成できる：

$$
View_V(P(x, w)) \approx S(x)
$$

---

## 離散対数型 ZKP（例）

公開情報：

$$
y = g^x
$$

### プロトコル

1. ランダム値を選ぶ  
$$
r \in \mathbb{Z}
$$

2. コミットメントを計算  
$$
t = g^r
$$

3. チャレンジ（ランダム）  
$$
c \leftarrow \text{random}
$$

4. 応答を計算  
$$
s = r + cx
$$

5. 検証  
$$
g^s = t \cdot y^c
$$

---

## 検証の意味（式変形）

$$
g^s = g^{r + cx}
$$

$$
= g^r \cdot (g^x)^c
$$

$$
= t \cdot y^c
$$


# ZKPパイプライン概要（Circom / snarkjs）

このノートは、Circom と snarkjs を使ったゼロ知識証明（ZKP）の基本的なワークフローを理解したい初学者向けのまとめです。

---

## 1. Witness Calculator（witness生成）

witness calculator は、コンパイルされた回路と入力データから **witness（証人データ）** を生成するためのものです。

- 回路（例：Circom）をコンパイルすると、以下のようなファイルが生成されます：
  - `.wasm`
  - `.js`

- これらを使って、入力データから witness を計算します。

witness には以下が含まれます：

- 公開入力（public inputs）
- 秘密入力（private inputs）
- 計算中のすべての中間値

### 関連ファイル

- `.wtns` → witness のバイナリ形式
- `.r1cs` → 制約システム（回路の数理的な定義）

> ※ `.r1cs` は witness ではなく、「回路の制約（数式）」を表すファイルです。

---

## 2. Proving Key / Verification Key（証明鍵と検証鍵）

これらは、ゼロ知識証明を「生成・検証」するために必要な鍵です。

- **Trusted Setup（信頼されたセットアップ）** の段階で生成されます
- 使用する証明方式（例：Groth16、PLONK）によって異なります

### 主なファイル

- `.zkey` → Proving Key（証明生成に使用）
- `.vkey.json` → Verification Key（検証に使用）

### 役割

- Prover（証明者）  
  → `.zkey` と witness を使って proof を生成する

- Verifier（検証者）  
  → proof と `.vkey` を使って正しさを検証する

---

## 3. Verifier Contract（検証コントラクト）

Verifier Contract は、ブロックチェーン上で proof を検証するためのスマートコントラクトです。

- 通常は Solidity（`.sol`）形式で生成されます
- snarkjs などのツールで自動生成されることが多いです

このコントラクトには：

- 検証ロジック
- Verification Key（`.vkey`）

が含まれています。

### 使用の流れ

1. ユーザーが proof を送信
2. コントラクトが検証
3. 正しければ「valid」、そうでなければ「invalid」

---

## パイプライン概要


---

## まとめ

- witness = 入力 + 中間計算を含むすべての値
- `.r1cs` = 回路の制約（数式）
- `.zkey` = 証明生成用の鍵
- `.vkey` = 検証用の鍵
- Contract = オンチェーンでの検証機構

---

## 参考（任意）

- Circom
- snarkjs



