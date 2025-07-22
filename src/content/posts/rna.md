---
title: 'ENN for Roman Numeral Analysis'
pubDate: '2025-03-19'
---

## The Task: Roman numeral analysis (RNA)
## Roman Numeral Analysis

**Roman Numeral Analysis (RNA)** is a method used in Western music theory to describe the harmonic function of chords relative to a given key. It abstracts away from absolute pitches and focuses instead on scale degrees and functional relationships within a tonal framework.

### Definition

Given a tonal center (key), each chord is assigned a Roman numeral that reflects its root's position within the diatonic scale of the key.  
- **Major chords** are denoted by uppercase numerals (e.g., **I**, **IV**, **V**).  
- **Minor chords** are indicated with lowercase numerals (e.g., **ii**, **iii**, **vi**).  
- **Diminished** and **augmented** chords are marked with additional symbols (e.g., **vii°**, **V+**).

### Notation Conventions

- Roman numerals represent the root scale degree of the chord.
- Case indicates chord quality:
  - Uppercase: Major
  - Lowercase: Minor
- Additional symbols:
  - `°` (e.g., **vii°**): Diminished
  - `+` (e.g., **V+**): Augmented
  - `6`, `6/4`, `4/2`, etc.: Inversion indicators
  - `/X` (e.g., **V/V**): Secondary function (tonicization)

### Analysis Process

The process of Roman Numeral Analysis involves the following steps:

1. **Establish the Key**: Determine the tonal center of the passage, often from the key signature and cadential patterns.
2. **Identify the Chords**: Determine the notes in each chord and their voicings.
3. **Root and Quality**: Identify the root of each chord and its quality (major, minor, diminished, etc.).
4. **Assign Roman Numerals**: Map each chord to a Roman numeral relative to the current key, using appropriate case and symbols.
5. **Mark Non-Diatonic Chords**: Identify and label tonicizations (e.g., **V/ii**), modulations, and chromatic chords using contextual analysis.
6. **Track Key Changes**: When modulation occurs, reset the tonal center and repeat the analysis in the new key.

### Example

In the key of **C major**:

```
Chord progression: C   G   Am   D7   G
Roman numerals:   I   V   vi   V/V  V
```

Here, **D7** functions as a secondary dominant (the dominant of G), briefly tonicizing the dominant **G**, which is then analyzed as **V** in C major.

### Applications

Roman Numeral Analysis is essential in:

- Understanding harmonic function and progression
- Comparing analogous progressions across different keys
- Analyzing form and phrase structure in tonal music
- Assisting in composition and improvisation


--- 
# Equivariant Neural Networks and Their Application to Roman Numeral Analysis

## 1. Formal Definition of Equivariant Neural Networks

An **equivariant neural network** is a model designed to preserve the **symmetry** of a structured input domain. Formally, a function $f: \mathcal{X} \to \mathcal{Y}$ is *equivariant* with respect to a group $G$ acting on $\mathcal{X}$ and $\mathcal{Y}$, if:

$$
f(T_g x) = T_g f(x), \quad \forall g \in G, \, x \in \mathcal{X}
$$

Where:
- $G$ is a group representing transformations (e.g., rotations, permutations).
- $T_g$ is a transformation of an input or output under group action $g \in G$.
- $f$ is the function (e.g., neural network layer) that commutes with the group action.

This means that applying a transformation to the input and then passing it through the network yields the same result as passing the input through the network and then transforming the output.

---

## 2. Application to Roman Numeral Analysis (RNA)

In **Roman Numeral Analysis**, the goal is to assign each harmonic region a label like **I**, **V**, **viio7**, etc., relative to a **local key**. RNA depends on relative pitch classes and functional harmony, which are **invariant or equivariant** under:

- **Pitch class transposition** (cyclic group $\mathbb{Z}_{12}$)
- **Inversion** (optional, depending on the task)
- **Time shifting** (if considering phrase alignment)
- **Voice permutation** (order of simultaneous notes)

### 2.1 Group Symmetry in Music

For RNA, we are primarily interested in **transposition-equivariance** over the pitch class domain:

- A C major chord in C major key labeled as "I"
- The same chord shape transposed to D major would still be "I" under transposition

Let $G = \mathbb{Z}_{12}$, acting on pitch classes:

$$
T_g(p) = (p + g) \mod 12
$$

The model should satisfy:

$$
f(T_g(x)) = T'_g(f(x))
$$

where $T_g$ acts on input notes, and $T'_g$ shifts the predicted Roman numeral root by $g$.

### 2.2 Equivariant Neural Network Design

To model this symmetry, use $\mathbb{Z}_{12}$-equivariant neural networks, such as:

- **Equivariant convolutions** over pitch classes
- **Group-convolutional networks** (e.g., steerable CNNs, harmonic networks)
- **Invariant linear layers** using shared weights over group orbits

Example:
- Encode pitch content as a 12-dimensional binary vector
- Apply group-equivariant filters over the 12-dimensional cyclic space

### 2.3 Benefits in RNA

- **Data efficiency**: Less need to see all keys during training
- **Interpretability**: Functionally correct responses under key transposition
- **Generalization**: Better transfer across musical contexts

---

## 3. Summary Table

| Concept                     | Formal Notation                         | Musical Analogy                        |
|----------------------------|------------------------------------------|----------------------------------------|
| Equivariance               | $f(T_g x) = T_g f(x)$                    | Transpose input → transpose output     |
| Group                      | $G = \mathbb{Z}_{12}$                    | 12-tone transposition group            |
| Input                      | Note/chord sequences as pitch sets       | e.g., [C, E, G]                        |
| Output                     | Roman numeral relative to local key      | e.g., "I", "V7", "iiø65"               |
| Network design             | $\mathbb{Z}_{12}$-equivariant layers     | Equivariant to key transposition       |
---
<!-- 
## Ref

- [KaTeX Documentation](https://katex.org/docs/supported.html) -->
