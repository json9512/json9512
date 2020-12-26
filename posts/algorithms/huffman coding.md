[Huffman coding compression](https://www.techiedelight.com/huffman-coding/)
# Huffman Coding
- algorithm to compress data
- containes two types of node: 1. leaf 2. internal
- all nodes contain the character and the weight (frequency of occurence)
- internal nodes contain character weight and links the two child nodes
- as a common convention, bit 0 is noted as left child, bit 1 is noted as the right child

# Algorithm
1. Create a leaf node for each character and add them to the priority queue (node with the lowest frequency will have the highest priority)
2. While there is more than one node in the queue:
    - Remove the two nodes of the highest priority from the queue
    - Create a new internal node with these two nodes as children and with a frequency equal to the sum of the two nodes' frequencies
        - eg. 
        - ![image](https://www.techiedelight.com/wp-content/uploads/2016/11/Huffman-Coding-1.png)
        - ![image](https://www.techiedelight.com/wp-content/uploads/2016/11/Huffman-Coding-3.png)
    - Add the new node to the priority queue
3. The remaining node is the root node and the tree is complete

The final Huffman tree:<br>
![image](https://www.techiedelight.com/wp-content/uploads/2016/11/Huffman-Coding-6.png)

# Code
```python
import heapq

def isLeaf(root):
    return root.left is None and root.right is None

# A tree node
class Node:
    def __init__(self, char, freq, left=None, right=None):
        self.char = char
        self.freq = freq
        self.left = left
        self.right = right
        self.text = "" # for root node only
    
    # Override the __lt__() function to make 'Node' work with priority queue
    # such that the highest priority item has the lowest frequency
    def __lt__(self, other):
        return self.freq < other.freq

# Traverse the Huffman Tree and store the Huffman codes in dictionary
def encode(root, string, huffman_code):
    if root is None:
        return 

    # if there is a leaf node
    if isLeaf(root):
        huffman_code[root.char] = string if len(string) > 0 else '1'
    
    encode(root.left, string + '0', huffman_code)
    encode(root.right, string + '1', huffman_code)

# Traverse the Huffman Tree and decode the encoded string
def decode(root, index, string):
    if root is None:
        return index
    
    # if leaf node
    if isLeaf(root):
        return index, root.char
    
    index += 1
    root = root.left if string[index] == '0' else root.right
    return decode(root, index, string)

# Builds Huffman Tree and decodes the given input
def buildHuffmanTree(text):

    # base case: empty string
    if len(text) == 0:
        return
    
    # count frequency of occurrence of each character
    # and store in dictionary
    freq = {i: text.count(i) for i in set(text)}

    # Create priority queue to store live nodes of the Huffman tree
    pqueue = [Node(k, v) for k, v in freq.items()]
    heapq.heapify(pqueue)

    # repeat until there is more than one node in the queue
    while len(pqueue) != 1:
        # Remove the two nodes of the highest priority
        # from the queue
        left = heapq.heappop(pqueue)
        right = heapq.heappop(pqueue)

        # Create new internal node with these two child nodes
        # with frequency weight summed
        # Add the created node to the priority queue
        total = left.freq + right.freq
        heapq.heappush(pqueue, Node(None, total, left, right))
    
    # root stores pointer to the root of Huffman Tree
    root = pqueue[0]
    root.text = text
    return root

# encodes the given Huffman tree with its text and returns the Huffman encoded dictionary
def huffmanEncode(root):
    huffmanCode = {}
    encode(root, "", huffmanCode)
    return huffmanCode

# Decodes the given tree's huffman encoded string (eg. 010) to original string (eg. 'abc')
def decodeHuffmanCode(root, encoded):
    decoded = ""
    if isLeaf(root):
        # special case: inputs like a, aa, aaa
        while root.freq > 0:
            decoded += root.char
            root.freq -= 1
    else:
        # Traverse the huffman tree 
        # decode the string
        index = -1
        while index < len(encoded) -1:
            index, char = decode(root, index, encoded)
            decoded += char 
    return decoded

def calcPercentage(text, encoded_string):
    og_bits = len(text)*8
    new_bits = len(encoded_string)
    increase = new_bits - og_bits
    return abs((increase/og_bits)*100)

def testCode(text):
    root = buildHuffmanTree(text)
    huffman_code_dict = huffmanEncode(root)

    print("Huffman Coding are: \n", huffman_code_dict)
    print("Original string is: \n", text)

    # print the original string encoded
    encoded_string = [huffman_code_dict.get(c) for c in text]
    encoded_string = ''.join(encoded_string)
    print("Encoded string is: \n", encoded_string)
    decoded = decodeHuffmanCode(root, encoded_string)
    print("Decoded string is: \n", decoded)

    print("\nThe total bits required for the original string was: "
        +"{}x8={} bits [8 bits, 1 byte required for storing a single charater]".format(len(text), len(text)*8))
    print("The encoded string has a bit size of : {} bits".format(len(encoded_string)))
    print(f"Compressed about {calcPercentage(text, encoded_string):.2f}% of data")

if __name__ == "__main__":
    text = "Huffman coding is a data compression algorithm."
    testCode(text)
'''
Huffman Coding are:
 {'.': '00000', 'H': '00001', 'r': '0001', 'g': '0010', 'e': '00110', 'l': '00111', 'a': '010', ' ': '011', 
 'm': '1000', 'h': '10010', 'c': '10011', 'n': '1010', 's': '1011', 'd': '11000', 'f': '11001', 'o': '1101', 
 'p': '111000', 'u': '111001', 't': '11101', 'i': '1111'}
Original string is:
 Huffman coding is a data compression algorithm.
Encoded string is:
 000011110011100111001100001010100111001111011100011111010001001111111011011010011110000101110101001110011110
 11000111000000100110101110111111110110100110100011100101101000111111110110010100000000
Decoded string is:
 Huffman coding is a data compression algorithm.

The total bits required for the original string was: 47x8=376 bits [8 bits, 1 byte required for storing a single charater]
The encoded string has a bit size of : 194 bits
Compressed about 48.40% of data
'''
```

Efficient priority queue requires `O(log n)` time per insertion and a complete binary tree with `n` leaves have `2n-1` nodes.

Thus, Huffman algorithm operates in `O(n log n)` time where `n` is the number of characters
