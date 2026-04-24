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




# ZKP Pipeline Overview (Circom / snarkjs)

This note is for beginners trying to understand the ZKP workflow using Circom and snarkjs.

---

## 1. Witness Calculator

The witness calculator is used to generate the **witness** from input data based on a compiled circuit.

- After compiling a circuit (e.g., with Circom), you typically get:
  - `.wasm`
  - `.js`

- These are used to compute the witness from given inputs.

The witness includes:
- Public inputs
- Private inputs
- All intermediate values of the computation

### Related files

- `.wtns` → Binary format of the witness
- `.r1cs` → Constraint system (the mathematical representation of the circuit)

> Note: `.r1cs` defines the circuit constraints, not the witness itself.

---

## 2. Proving and Verification Keys

These keys are required to generate and verify zero-knowledge proofs.

They are generated during the **trusted setup** phase, depending on the proving system (e.g., Groth16, PLONK).

### Key files

- `.zkey` → Proving key (used to generate proofs)
- `.vkey.json` → Verification key (used to verify proofs)

### Roles

- Prover:
  - Uses `.zkey` + witness → generates a proof

- Verifier:
  - Uses proof + `.vkey` → verifies correctness

---

## 3. Verifier Contract

The verifier contract is a smart contract used to verify proofs on-chain.

- Usually generated in Solidity (`.sol`)
- Often auto-generated using tools like snarkjs

The contract contains:
- Verification logic
- Embedded verification key (`.vkey`)

### Usage

1. A user submits a proof
2. The contract verifies it
3. Returns valid / invalid

---

## Pipeline Overview


---

## Summary

- Witness = all computation values (inputs + intermediate)
- `.r1cs` = circuit constraints
- `.zkey` = proving key
- `.vkey` = verification key
- Contract = on-chain verifier

---

## References (optional)

- Circom
- snarkjs

