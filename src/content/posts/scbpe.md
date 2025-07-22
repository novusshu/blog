---
title: 'Simultaneity-Centric Byte Pair Encoding'
pubDate: '2024-07-06'
---

Simultaneity Combinatorial Byte Pair Encoding (SCBPE), a novel tokenization method designed specifically for symbolic music generation and understanding with Transformers. Unlike conventional approaches that treat music as a simple linear sequence of tokens (similar to text), SCBPE explicitly models the simultaneity and rich texture inherent in musical compositions. By aligning token sequences with the actual, simultaneous structure of music, SCBPE creates a more efficient embedding space, reduces sequence length, and enables more stable and coherent music generation. Experimental results show that SCBPE significantly improves both the quality of generated music and the consistency of musical styles, while also enhancing performance in music understanding tasks.

---

The contributions of SCBPE are highlighted as follows:
- Efficient Embedding Space: By combining multiple aspects of each note into a single embedding and explicitly modeling simultaneity, SCBPE reduces sequence length and enhances the utilization of the embedding space.
- Improved Generation Quality: SCBPE addresses instability in generated music styles by maintaining the inherent simultaneity and rich texture of music, leading to more coherent and stylistically consistent outputs.
- Enhanced Music Understanding: The explicit representation of simultaneity in SCBPE facilitates better music understanding tasks, providing a more accurate and comprehensive analysis of musical compositions.

--- 

Combinatory BPE pseudo-code

We introduce three modifications to the traditional BPE algorithm to accommodate the unique characteristics of SimulMI encoding. First, we do not combine duration events into new tokens, as we aim to preserve the pair structure as much as possible. Second, we use combinatorics to identify the most common pitch combinations, because unlike letters in a sentence, the order of pitches within a pitch group is irrelevant. Third, we apply BPE exclusively within each pitch group, treating each pitch group as a single unit during both tokenizer training and tokenization. This approach minimizes syntactic errors caused by mixed token types.

```algorithm
Input: 
    Base vocabulary V
    Target vocabulary size N
    Dataset X

Output: 
    Expanded vocabulary V with size ≤ N

while |V| < N:
    1. Find s = {t₁, t₂} ∈ V², from X, the most recurrent token combination
    2. Add a new token t in V, mapping to s
    3. Substitute every occurrence of s in X with t

return V
```


