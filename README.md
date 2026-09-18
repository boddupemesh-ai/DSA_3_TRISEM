# GeneScan – DNA Mutation & Disease Variant Detector

## 📌 Project Overview

**GeneScan** is a Java-based bioinformatics application that compares a healthy reference DNA/protein sequence with a patient sample to identify sequence differences.

The project uses **String Algorithms** and **Dynamic Programming** to perform sequence analysis and detect possible mutations such as:

* Substitution mutations
* Insertions
* Deletions
* Conserved sequence regions

> **Note:** This project uses simplified and illustrative biological sequences for educational purposes. It is not a diagnostic or clinical tool.

---

## 🎯 Objectives

* Compare healthy and patient DNA/protein sequences.
* Find the longest exact common region between two sequences.
* Perform local sequence alignment.
* Calculate alignment scores and sequence similarity.
* Detect mismatches and gaps.
* Classify sequence differences as substitutions or indels.
* Analyze multiple patient samples efficiently.

---

## 🧬 Algorithms Used

### 1. Suffix Array

The project creates a **Suffix Array** from the combined healthy and patient sequences.

A suffix is a substring that starts at a particular position and continues until the end of the sequence.

The suffixes are sorted and used to efficiently compare different regions of the sequences.

### 2. Kasai LCP Algorithm

**Kasai's Longest Common Prefix (LCP)** algorithm is used along with the Suffix Array.

It calculates how many characters are common at the beginning of two neighboring suffixes.

The project uses this to find the **Longest Exact Common Substring** between the healthy and patient sequences.

For example, in the HBB DNA example, the project identifies:

```text
ATGGTGCACCTGACTCCTG
```

as the longest exact common region.

---

### 3. Smith–Waterman Algorithm

The **Smith–Waterman algorithm** is the main sequence alignment algorithm used in the project.

It performs **local alignment**, meaning it searches for the best matching region between two sequences.

The algorithm creates a **2D Dynamic Programming matrix**.

For every cell, it considers:

* Diagonal → Match or mismatch
* Up → Gap
* Left → Gap
* Zero → Start a new local alignment

The scoring values can be configured by the user.

Example:

```text
Match    = +2
Mismatch = -1
Gap      = -2
```

The highest value in the matrix represents the best local alignment score.

---

## 🔄 Algorithm Workflow

```text
Healthy Sequence + Patient Sequence
                ↓
        Sequence Validation
                ↓
      Suffix Array Construction
                ↓
          Kasai LCP Algorithm
                ↓
    Longest Exact Common Substring
                ↓
       Smith–Waterman Alignment
                ↓
        Dynamic Programming Matrix
                ↓
              Traceback
                ↓
       Aligned Sequences Generated
                ↓
      Match / Mismatch / Gap Count
                ↓
          Mutation Detection
```

---

## 🔍 Mutation Detection

After Smith–Waterman alignment, the aligned sequences are compared character by character.

### Match

If both characters are the same:

```text
A
A
```

It is counted as a match.

### Substitution

If the characters are different:

```text
G
T
```

It is counted as a mismatch and reported as a substitution mutation.

### Insertion / Deletion

If one sequence contains a gap:

```text
ATCTTTGGT
ATC---GGT
```

the gap positions are reported as an insertion/deletion (indel).

---

## 📊 Output

The program displays:

* Healthy reference sequence
* Patient sample sequence
* Scoring parameters
* Longest exact common substring
* LCP length
* Smith–Waterman alignment score
* Aligned sequences
* Match indicators
* Number of matches
* Number of mismatches
* Number of gaps
* Percentage similarity
* Alignment region
* Execution time
* Detected mutation type

---

## 🧪 Example

### HBB DNA Sequence

The project compares:

```text
Healthy:
ATGGTGCACCTGACTCCTGAGGAGAAGTCT

Patient:
ATGGTGCACCTGACTCCTGTGGAGAAGTCT
```

Using:

```text
Match    = +2
Mismatch = -1
Gap      = -2
```

The output gives:

```text
Alignment Score   : 57
Matches           : 29
Mismatches        : 1
Gaps              : 0
Similarity        : 96.67%
```

The program therefore reports:

```text
1 substitution mutation
```

The project also includes an illustrative deletion case where the alignment contains three gap positions and the program reports an indel.

---

## 🧬 Protein-Level Analysis

GeneScan can also compare protein sequences.

For the beta-globin protein example, the program performs the same two-stage process:

```text
Suffix Array + Kasai LCP
            ↓
Smith–Waterman Alignment
            ↓
Mutation Analysis
```

The example produces:

```text
Matches      : 58
Mismatches   : 1
Gaps         : 0
Similarity   : 98.31%
```

---

## 📈 Batch Screening

The project also demonstrates batch screening using **100 patient DNA samples** against a healthy HBB reference sequence.

Each sample is processed using Smith–Waterman alignment and classified based on the detected sequence differences.

The demonstration output reports:

```text
Total Samples Screened     : 100
Mutation Detected          : 33
Normal                     : 67
Average Time / Sample      : 0.1247 ms
```

This demonstrates how the alignment algorithm can be repeatedly applied to multiple samples.

---

## ⚡ Performance Analysis

The project also measures Smith–Waterman execution time for different sequence sizes.

Example results:

| Sequence Size | Execution Time |
| ------------- | -------------: |
| 100 × 100     |       2.139 ms |
| 200 × 200     |       6.344 ms |
| 400 × 400     |      12.127 ms |
| 800 × 800     |      16.741 ms |
| 1600 × 1600   |      81.168 ms |

This demonstrates the increase in computation time as sequence length increases.

---

## 🛠️ Technologies Used

* **Java**
* **Dynamic Programming**
* **String Algorithms**
* **Suffix Array**
* **Kasai LCP**
* **Smith–Waterman Local Alignment**
* **2D Arrays**
* **Sequence Analysis**

---

