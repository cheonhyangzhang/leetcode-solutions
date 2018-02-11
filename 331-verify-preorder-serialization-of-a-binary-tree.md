# 331 Verify Preorder Serialization of a Binary Tree

### Problem:


One way to serialize a binary tree is to use pre-order traversal. When we encounter a non-null node, we record the node's value. If it is a null node, we record using a sentinel value such as #.
```
     _9_
    /   \
   3     2
  / \   / \
 4   1  #  6
/ \ / \   / \
# # # #   # #
```
For example, the above binary tree can be serialized to the string "9,3,4,#,#,1,#,#,2,#,6,#,#", where # represents a null node.

Given a string of comma separated values, verify whether it is a correct preorder traversal serialization of a binary tree. Find an algorithm without reconstructing the tree.

Each comma separated value in the string must be either an integer or a character '#' representing null pointer.

You may assume that the input format is always valid, for example it could never contain two consecutive commas such as "1,,3".

Example 1:
"9,3,4,#,#,1,#,#,2,#,6,#,#"
Return true

Example 2:
"1,#"
Return false

Example 3:
"9,#,#,1"
Return false


### Solutions:

```java
public class Solution {
    private int index = 0;
    public boolean isValidSerialization(String preorder) {
        String[] vals = preorder.split(",");
        if (vals.length % 2 == 0) {
            return false;
        }
        index = 0;
        return visit(vals) && index == vals.length;
    }
    private boolean visit(String[] vals) {
        if (index >= vals.length) {
            return false;
        }
        if (vals[index].equals("#")) {
            index ++;
            return true;
        }
        index ++;
        return visit(vals) && visit(vals);
    }
}
```

```java
public class Solution {
    private int index = 0;
    public boolean isValidSerialization(String preorder) {
        String[] vals = preorder.split(",");
        if (vals.length % 2 == 0) {
            return false;
        }
        Stack<String> s = new Stack<String>();
        for (int i = 0; i < vals.length; i ++) {
            s.push(vals[i]);
            while (s.size() >= 3) {
                String s1 = s.pop();
                String s2 = s.pop();
                String s3 = s.pop();
                if (s1.equals("#") && s2.equals("#") && !s3.equals("#")) {
                    s.push("#");
                }
                else {
                    s.push(s3);
                    s.push(s2);
                    s.push(s1);
                    break;
                }
            }
        }
        if (s.size() == 1 && s.pop().equals("#")) {
            return true;
        }
        else {
            return false;
        }
    }
}
```

```java
public class Solution {
    private int index = 0;
    public boolean isValidSerialization(String preorder) {
        String[] vals = preorder.split(",");
        if (vals.length % 2 == 0) {
            return false;
        }
        int diff = 1; // outdegree - indegree
        for (String s:vals) {
            diff --;
            if (diff < 0) {
                return false;
            }
            if (!s.equals("#")) {
                diff += 2;
            }
        }
        return diff == 0;
    }
}
```