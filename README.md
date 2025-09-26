### EX3 Implementation of GSP Algorithm In Python
### DATE: 19.09.2025
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
### Program:

```python
from collections import defaultdict
from itertools import combinations

def generate_candidates(dataset, k):
  c = defaultdict(int)
  for seq in dataset:
    flat_seq = [item for itemset in seq for item in itemset]
    for item in combinations(flat_seq, k):
        c[item] += 1
  return {item: support for item, support in c.items() if support >= min_support}

def gsp(dataset, min_support):
  k=1
  fp = defaultdict(int)
  seq = dataset
  while True:
    c=generate_candidates(seq, k)
    if not c:
      break
    k+=1
    fp.update(c)
  return fp

dataset1 = [
    [["a"],["b"],["c"], ["b","e"], ["c"],["f"],["g"], ["a","b","e"]],
    [["a"], ["d"], ["b", "c"], ["c"], ["f","g"],["c", "h"]],
    [["b"], ["c"], ["a","d"], ["e"], ["b"], ["f"], ["c", "d", "f", "g", "h"]],
    [["c"], ["e", "c"], ["e", "h"]]
]
dataset2 = [
    [["b","d"], ["c"], ["b"], ["a","c"]],
    [["b","f"], ["c","e"], ["b"], ["f","g"]],
    [["a","h"], ["b","f"], ["a"], ["b"], ["f"]],
    [["b","e"], ["c","e"], ["d"]],
    [["a"], ["b","d"], ["b"], ["c"], ["b"], ["a","d","e"]]
]

min_support = 3

frequent1 = gsp(dataset1, min_support)
frequent2 = gsp(dataset2, min_support)

print("Frequent Sequential Patterns for Dataset 1:")
if frequent1:
    for pattern, support in frequent1.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")

print("\nFrequent Sequential Patterns for Dataset 2:")
if frequent2:
    for pattern, support in frequent2.items():
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")
```
### Output:
<img width="746" height="1732" alt="image" src="https://github.com/user-attachments/assets/92638e43-e694-4a8b-a472-21da72191a12" />

### Visualization:
```python
import matplotlib.pyplot as plt
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

visualize_patterns_line(frequent1, 'dataset1')
visualize_patterns_line(frequent2, 'dataset2')
```
### Output:
<img width="989" height="590" alt="image" src="https://github.com/user-attachments/assets/747e65cc-23ef-42c4-8283-02489c45bbd0" />


### Result:
Thus GSP Algorithm in Python has been implemented successfully.
