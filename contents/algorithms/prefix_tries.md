# Prefix Trie
A prefix trie is a data structure that stores a set of strings arranged in a tree such that words with a shared prefix are contained within the same subtree

**Key ideas**
- The prefix trie is a rooted tree (not necessarily binary)
- Each edge is labelled with a character. Alternatively, each node can be labelled (except the root).
- A path from the root to a node in the trie corresponds to a prefix of a word in the trie
- A path from the root to an internal node of the trie corresponds to a common prefix of multiple strings
- The end of each word is indicated by a terminating character

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/19b42d90-1030-4ec2-a049-41174cec0704)

## Prefix trie: Insertion
Assuming that we are implementing our trie with an array, insertion will take O(n) time where n is the length of the query string. We have to insert our string character by character and at each character we have to check if it is already in the trie, if its not we add it to the trie and repeat until the string has been processed.

```
1: function INSERT(S[1..n])
2:   node = root
3:   for each character c in S[1..n] do
4:     if node has an edge for character c then
5:       node = node.get_child(c )
6:     else
7:       node = node.create_child(c
```

## Prefix trie: Lookup
To lookup up a string in the trie, we just follow the queried string character by character until we reach the end. If our string is not in the trie, one of the characters will be missing and therefore we return false. This will take O(n) time.

```
1: // Returns True if the trie contains a word that has S as a prefix
2: function LOOKUP(S[1..n])
3:   node = root
4:   for each character c in S[1..n] do
5:     if node has an edge for character c then
6:       node = node.get_child(c )
7:     else
8:       return false
9:   return true
```

## Prefix trie: String sorting
We can use a prefix trie to quickly sort a list of strings coming from a fixed size alphabet. Simply insert all of the strings into a prefix trie, then traverse the trie in lexographical order. Using the array-based implementation, the complexity of this algorithm is O(AT), where A is the size of the alphabet and T is the total length of all words in the trie.

```
1: function SORT_STRINGS(strings[1..n])
2:   for each string s in strings[1..n] do
3:     INSERT(s + ‘$’)
4:   TRAVERSE(root, "")
5:
6: function TRAVERSE(node, cur_string)
7:   if cur_strings ends with ‘$’ then // We are at the end of a string
8:     print (cur_string) // Can omit printing the ‘$’ character
9:   else
10:    for each child character c of node in alphabetical order do
11:      cur_string.append(c )
12:      TRAVERSE(node.get_child(c ), cur_string)
13:      cur_string.pop_back() // Remove the last character of cur_string
```
