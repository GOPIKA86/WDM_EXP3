### EX3 Implementation of GSP Algorithm In Python
#### NAME: GOPIKA A
#### REG NO: 212224100017
#### DATE: 03/08/2026
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
import matplotlib.pyplot as plt

def is_subsequence(candidate, sequence):
    i = 0
    for item in sequence:
        if i < len(candidate) and candidate[i] == item:
            i += 1
    return i == len(candidate)

def generate_L1(database, min_support):
    counts = defaultdict(int)

    for seq in database:
        for item in set(seq):
            counts[(item,)] += 1

    return {k: v for k, v in counts.items() if v >= min_support}

def generate_candidates(prev_patterns):
    prev_patterns = list(prev_patterns)
    candidates = set()

    for i in range(len(prev_patterns)):
        for j in range(len(prev_patterns)):
            p1 = prev_patterns[i]
            p2 = prev_patterns[j]

            if p1[1:] == p2[:-1]:
                candidates.add(p1 + (p2[-1],))

    return candidates

def count_support(database, candidates, min_support):
    support = defaultdict(int)

    for candidate in candidates:
        for sequence in database:
            if is_subsequence(candidate, sequence):
                support[candidate] += 1

    return {k: v for k, v in support.items() if v >= min_support}

def gsp(database, min_support):
    frequent_patterns = {}

    L = generate_L1(database, min_support)
    frequent_patterns.update(L)

    while L:
        candidates = generate_candidates(L.keys())
        L = count_support(database, candidates, min_support)
        frequent_patterns.update(L)

    return frequent_patterns

top_wear_data = [
    ["blouse", "t-shirt", "tank_top"],
    ["hoodie", "sweater", "top"],
    ["hoodie"],
    ["hoodie", "sweater"]
]

bottom_wear_data = [
    ["jeans", "trousers", "shorts"],
    ["leggings", "skirt", "chinos"]
]

party_wear_data = [
    ["cocktail_dress", "evening_gown", "blazer"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress", "formal_dress", "suit"],
    ["party_dress"],
    ["party_dress"]
]

min_support = 2

top_wear_result = gsp(top_wear_data, min_support)
bottom_wear_result = gsp(bottom_wear_data, min_support)
party_wear_result = gsp(party_wear_data, min_support)

print("Frequent Sequential Patterns - Top Wear:")
if top_wear_result:
    for pattern, support in sorted(top_wear_result.items()):
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")

print("\nFrequent Sequential Patterns - Bottom Wear:")
if bottom_wear_result:
    for pattern, support in sorted(bottom_wear_result.items()):
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")

print("\nFrequent Sequential Patterns - Party Wear:")
if party_wear_result:
    for pattern, support in sorted(party_wear_result.items()):
        print(f"Pattern: {pattern}, Support: {support}")
else:
    print("No frequent sequential patterns found.")
```
### Output:
<img width="787" height="356" alt="image" src="https://github.com/user-attachments/assets/40019b12-d4a0-482f-9a83-90771da622c6" />


### Visualization:
```python
import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
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

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(top_wear_result, 'Top Wear')
visualize_patterns_line(bottom_wear_result, 'Bottom Wear')
visualize_patterns_line(party_wear_result, 'Party Wear')
```
### Output:
<img width="1046" height="621" alt="image" src="https://github.com/user-attachments/assets/44af6009-bc91-49f6-b430-87e86d2141c1" />

<img width="1045" height="587" alt="image" src="https://github.com/user-attachments/assets/2d4e7284-f7b8-42c5-89fe-243ee403efe4" />

### Result:
Thus the implementation of the GSP algorithm in python has been successfully executed.

