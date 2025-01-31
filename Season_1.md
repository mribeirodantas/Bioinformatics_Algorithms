## 🧬 Season 1 - Diggin down deep
### 🐍 Ep 1 - Let's calcualte the basic Pattern given in the series of Genetic sequence code
🛠️ Dataset code
```Python
text = 'ATGCATATGACTACTAGATACTGATACTGATACATA'
pattern = 'ATA'
print(len(pattern))
print(len(text))
print(text[0:3])
```

Let's suppose this is the basic dataset given to us, in which we are asked to find the pattern "ATA" from the Sequence i.e. how much time this particlaur motif occurs or is present in the Parent sequence.

🛠️ Program code
```Python
text = 'ATGCATATGACTACTAGATACTGATACTGATACATA'
pattern = 'ATA'
def PatternCount(Text, Pattern):
    count = 0
    for i in range(len(Text)-len(Pattern)+1):
        if Text[i:i+len(Pattern)] == Pattern:
            count = count+1 
    return count 
print(PatternCount(text, pattern))
```
Output of this code of line is "5" ie. 5 times ATA motif exist in the whole genome sequence 

### 🐍 Ep 2 - Understanding the Frequency map 
In this episode, we take the next step in understanding the occurrence of various patterns (k-mers) within a genetic sequence. A frequency map is a dictionary that maps each k-mer to the number of times it appears in the sequence. This is particularly useful for finding motifs or repeated patterns in DNA sequences.

🛠️ Program code 
```Python
def FrequencyMap(Text, k):
    freq = {}
    n = len(Text)
    for i in range(n - k + 1):
        Pattern = Text[i:i + k]
        if Pattern in freq:
            freq[Pattern] += 1
        else:
            freq[Pattern] = 1
    return freq

# Example usage
text = 'ACGTTGCATGTCGCATGAGCATGAGAGCT'
k = 3
print(FrequencyMap(text, k))
```
Output of this code looks something like this
```Python
{'ACG': 1, 'CGT': 1, 'GTT': 1, 'TTG': 1, 'TGC': 2, 'GCA': 3, 'CAT': 3, 'ATG': 3, 
 'TGT': 1, 'GTC': 1, 'TCG': 1, 'CGC': 1, 'TGA': 2, 'GAG': 2, 'AGA': 1, 'GCT': 1}
```
where, The function takes a DNA sequence (``Text``) and k-mer length (``k``) as input, extracts all k-mers, and returns a dictionary mapping each k-mer to its count.

### 🐍 Ep 3 - Most Frequent K-mers
Now let's understand how this magic runs in the world of Bioinfomatics, here we will be using 2 main functions, one of which we already understood earlier:
1. ``FrequencyMap`` - To calculate the frequency of all k-mers in the given sequence. (we understood earlier)
2. ``FrequentWords`` - To identify and return the most frequent k-mers.

🛠️ Program Code
```Python
def FrequencyMap(Text, k):
    freq = {}
    n = len(Text)
    for i in range(n - k + 1):
        Pattern = Text[i:i + k]
        if Pattern in freq:
            freq[Pattern] += 1
        else:
            freq[Pattern] = 1
    return freq

def FrequentWords(Text, k):
    words = []
    freq = FrequencyMap(Text, k)
    m = max(freq.values())  # Find the maximum frequency
    
    for key in freq:
        if freq[key] == m:
            words.append(key)  # Append k-mers with maximum frequency
    
    return words
# Example usage
Text = 'ACGTTGCATGTCGCATGAGCATGAGAGCT'
k = 3
```
Output of this code looks something like this
```Python
['GCA', 'CAT', 'ATG']
```
By combining a frequency map with a simple search for the maximum value, we can quickly identify the most frequent patterns (k-mers) in any DNA sequence. 
We found a very specific type of Output where this motif seq have the most occurance in the Parent genomic sequence.

This is a fundamental step for motif discovery and genomic analysis. 

### 🐍 Ep 4 - Complementary DNA String
Now I know very well that ``BioPython`` provides a very short/single line of code to do this i.e. ``Bio.Seq.complement()``  but just to get hold of the python and the essence of how does python interpret this single line in ``Biopython library`` would be very intresting to understand.

Complementing is bascially:
- **A** ↔ **T**
- **C** ↔ **G**

🛠️ Program Code
```Python
def Complement(Pattern):
    compl = ''
    for i in Pattern:
        if i == 'A':
            compl = compl + 'T'
        elif i == 'T':
            compl = compl + 'A'
        elif i == 'C':
            compl = compl + 'G'
        elif i == 'G':
            compl = compl + 'C'
    return compl

# Example usage
print(Complement('ACGTTGCATGTCGCATGAGCATGAGAGCT'))
```
Output should look something like this ``TGCAACGTACAGCGTACTCGTACTCTCGA`` which is a complementary sequence to the given sequence

### 🐍 Ep 5 - Pattern Matching in DNA Sequence
In this episode, we will explore how to find all positions where a given pattern appears in a DNA sequence. This is very much similar to that of the Frequency counter i.e. ``MostFrequentK-Mer`` but we are trying to find exact positions where this patterns exist in the particular parent sequence (``Genome``).

We will use the ``PatternMatching`` function to search for a specified pattern in the given sequence (``Genome``), and return all positions where the pattern starts.

🛠️ Program Code
```Python
def PatternMatching(Pattern, Genome):
    Positions = []  # Output list to store positions
    for i in range(len(Genome) - len(Pattern) + 1):
        if Genome[i:i+len(Pattern)] == Pattern:  # Check for the match
            Positions.append(i)  # Append position if match found
    return Positions

# Example usage
text = 'CGCGATACGTTACATACATGATAGACCGCGCGCGATCATATCGCGATTATC'
pattern = 'CGCG'
print(PatternMatching(pattern, text))
```

Output look something like this for particular dataset ``[0, 16, 28, 38]``, where this function helps identify the starting positions of a pattern within a DNA sequence, which is crucial for many bioinformatics tasks like motif finding and sequence alignment.
