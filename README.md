# Huffman Coding Using Python

## Aim
To implement Huffman Coding using Python for data compression by generating Huffman codes based on character frequencies.

---

## Description
Huffman Coding is a lossless data compression algorithm.  
In this experiment, a Huffman Tree is constructed based on the frequency of characters in a given string. Characters with higher frequency are assigned shorter binary codes, while characters with lower frequency are assigned longer binary codes.

---

## Algorithm
1. Read the input string.
2. Calculate the frequency of each character.
3. Create nodes for all characters.
4. Sort nodes based on frequency.
5. Combine two nodes with the lowest frequency.
6. Repeat until a single Huffman tree is formed.
7. Generate Huffman codes by traversing the tree.
8. Display the Huffman codes.

---

## Program
```python
# Get the input String
string = "BCAADDDCCACACAC"

# Create tree nodes
class NodeTree(object):

    def __init__(self, left=None, right=None):
        self.left = left
        self.right = right

    def children(self):
        return (self.left, self.right)

    def nodes(self):
        return (self.left, self.right)

    def __str__(self):
        return '%s_%s' % (self.left, self.right)


# Main function to implement huffman coding
def huffman_code_tree(node, left=True, binString=''):

    if type(node) is str:
        return {node: binString}

    (l, r) = node.children()

    d = dict()
    d.update(huffman_code_tree(l, True, binString + '0'))
    d.update(huffman_code_tree(r, False, binString + '1'))

    return d


# Calculate frequency of occurrence
freq = {}

for c in string:
    if c in freq:
        freq[c] += 1
    else:
        freq[c] = 1

freq = sorted(freq.items(), key=lambda x: x[1], reverse=True)

nodes = freq

while len(nodes) > 1:
    (key1, c1) = nodes[-1]
    (key2, c2) = nodes[-2]

    nodes = nodes[:-2]

    node = NodeTree(key1, key2)
    nodes.append((node, c1 + c2))

    nodes = sorted(nodes, key=lambda x: x[1], reverse=True)


# Print the characters and its huffmancode
huffmanCode = huffman_code_tree(nodes[0][0])

print(' Char | Huffman code ')
print('--------------------')

for (char, frequency) in freq:
    print(' %-4r | %12s' % (char, huffmanCode[char]))
```py
 Char | Huffman code
--------------------
 'A'  |          11
 'C'  |          10
 'D'  |         011
 'B'  |         010
```
## Result

Thus, Huffman Coding was successfully implemented using Python and the Huffman codes for the given characters were generated successfully.
