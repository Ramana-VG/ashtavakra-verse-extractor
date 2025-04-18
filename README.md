# Ashtavakra Gita Verse Extractor

This Python script extracts verses and their indices from the [Ashtavakra Gita](https://gretil.sub.uni-goettingen.de/gretil/corpustei/transformations/plaintext/sa_aSTAvakragItA.txt) in plain text format.

## Problem Statement

Given a text like:
kathaṃ jñānam avāpto 'ti kathaṃ muktir bhaviṣyati
vairāgyaṃ ca kathaṃ prāptam etad brūhi mama prabho // Avg_1.1

Extract:
- The **verse** (2 lines of Sanskrit)
- The **verse index** (e.g. `1.1`)

### Output Format (JSON)
{
  "verse": "kathaṃ jñānam avāpto 'ti kathaṃ muktir bhaviṣyati\n vairāgyaṃ ca kathaṃ prāptam etad brūhi mama prabho",
  "index": "1.1"
}

## Solution Strategy

### 1. Understand the Structure

Each verse is written in two lines, and only the **second line** contains the index marker `// Avg_1.x`.

### 2. Pattern Matching with Regex

Use a regular expression to match lines with the pattern:

regex
(.*?)\s*//\s*Avg_(\d+\.\d+)

This pattern:

Capture the second line of the verse (before //)

Extract the verse index (e.g., "1.1")

### 3. Combine with the Previous Line
When we find a matching line, we take:

The previous line from the list (as the first half of the verse)

The current line (before index, as second half) And combine them into a full verse.

### 4. Save the verses as a JSON file with proper Unicode support


