# Suffix trees
A suffix tree is a compact trie containing all of the suffixes of a string. We motivate suffix trees as a solution to the *pattern matching* problem. It breaks down a string into all its possible suffixes and store it as a trie.
![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/d1925219-be15-46b5-9ab1-b21182f78fe0)

## The pattern matching problem
Suffix tries allow us to solve the pattern matching problem in O(m) time, where m is the pattern length, as we can just check if the pattern P is a prefix in the trie. 

## Compacting the trie into a tree
Since a string of length n has n suffixes, and each length has length O(n), a suffix trie will take O(n^2) space. This is why suffix trees are stored as compact tries, which will just take O(n) space.

![image](https://github.com/awat0045/FIT2004-notes/assets/140218451/60587041-ca4e-4aed-9744-e19597a0702a)

## Building a suffix trie
The easiest way to build a suffix tree is to build the suffix trie in O(n^2) time then compress it into a suffix tree. There is an algorithm that can construct a suffix tree in O(n) time called Ukkonen's algorithm, however it is outside the scope of this unit.
