```java
class WordDictionary {
	class TrieNode {
		boolean isWord;
		HashMap<Character, TrieNode> nexts;

		public TrieNode() {
			nexts = new HashMap<Character, TrieNode>();
		}
	}

	private TrieNode root;
	private boolean flag =false;

	/** Initialize your data structure here. */
	public WordDictionary() {
		root = new TrieNode();
	}

	/** Adds a word into the data structure. */
	public void addWord(String word) {
		char[] s = word.toCharArray();

		TrieNode p = root;
		int i = 0, n = s.length;

		// traverse existing
		while (i < n) {
			TrieNode next = p.nexts.get(s[i]);
			if (next != null) {
				p = next;
				i ++;
			} else {
				break;
			}
		}

		// append new nodes
		while (i < n) {
			TrieNode newTrie = new TrieNode();
			p.nexts.put(s[i], newTrie);
			p = newTrie;
			i ++;
		}

		// set word end
		p.isWord = true;
	}

	public boolean search(String word) {
		return help(word.toCharArray(), 0, root);
	}

  //如果顺序下来的时候可以不用递归，p是之前最后的结点
	public boolean help(char[] words, int i, TrieNode p) {
		if (i == words.length) return p.isWord;
        
        while(i<words.length){
            if ((words[i]) == '.') {
                //对于每一个可能都是相同的可能性，用递归
                for (Map.Entry<Character, TrieNode> x : p.nexts.entrySet()) {
                    if (help(words, i + 1, x.getValue())) return true;
                }
                //如果跳出循环就是false了
                return false;
            } else {
                TrieNode child = p.nexts.get(words[i++]);
                if (child == null) {
                    return false;
                }
                p = child;
            }
        }

		return p.isWord;
	}
  
  //也可以用递归
  public boolean help(char[] words, int i, TrieNode p) {
		if (i == words.length) return p.isWord;

		if ((words[i]) == '.') {
			for (Map.Entry<Character, TrieNode> x : p.nexts.entrySet()) {
				if (help(words, i + 1, x.getValue())) return true;
			}
			return false;
		} else {
			TrieNode child = p.nexts.get(words[i]);
			if (child == null) {
				return false;
			}
			p = child;
		}

		return help(words, i + 1, p);
	}
}
```
