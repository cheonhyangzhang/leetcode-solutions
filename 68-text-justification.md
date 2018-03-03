# 68 Text Justification

### Problem
Given an array of words and a length L, format the text such that each line has exactly L characters and is fully (left and right) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no extra space is inserted between words.

For example,
words: ["This", "is", "an", "example", "of", "text", "justification."]
L: 16.

Return the formatted lines as:
```
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```
Note: Each word is guaranteed not to exceed L in length.

### Solutions

```java
public class Solution {
    public List<String> fullJustify(String[] words, int L) {
        List<String> res = new ArrayList<String>();
        List<String> helper = new ArrayList<String>();
        int curL = 0;
        for (int i = 0; i < words.length; i ++){
            int wordL = words[i].length();
            if (curL != 0){
                curL +=1;
            }
            curL += wordL;

            if (curL > L){
                curL = curL - wordL - 1;
                int num = helper.size();
                int totalSpaceNum = 0;
                int eachSpaceNum = 0;
                String eachSpace = "";
                if (num !=1) {
                    totalSpaceNum = L - curL + num - 1;
                    eachSpaceNum = totalSpaceNum / (num - 1);
                    for (int k = 0; k < eachSpaceNum; k ++){
                        eachSpace += " ";
                    }
                }
                String plusSpace = eachSpace + " ";
                //num - 1's space
                int diff = totalSpaceNum - eachSpaceNum *(num-1);

                String add = "";
                for (int j = 0; j < helper.size(); j ++){
                    if (j == 0){
                        add +=helper.get(j);
                    }
                    else if (j <= diff){
                        add = add + plusSpace + helper.get(j);
                    }
                    else{
                        add = add + eachSpace + helper.get(j);
                    }
                }
                addRes(res, L, add);
                helper.clear();
                curL = 0;
                i --;
            }
            else if (curL == L){
                helper.add(words[i]);
                String add = "";
                for (int j = 0; j < helper.size(); j ++){
                    if (j == 0){
                        add +=helper.get(j);
                    }
                    else{
                        add = add + " " + helper.get(j);
                    }
                }
                addRes(res, L, add);
                helper.clear();
                curL = 0;
            }
            else{
                //curL < L
                helper.add(words[i]);
            }
        }//for i

        if (!helper.isEmpty()){
            String add = "";
            for (int k = 0; k < helper.size(); k ++){
                if (k == 0){
                    add += helper.get(k);
                }
                else{
                    add = add + " " + helper.get(k);
                }
            }
            addRes(res, L, add);
        }
        return res;
    }
    private void addRes(List<String> res, int L, String add){
        int append = L - add.length();
        for (int k = 0; k < append; k ++){
            add += " ";
        }
        res.add(add);
    }
}
```

```java
class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> line = new LinkedList<>();
        List<String> res = new LinkedList<>();
        int count = 0;
        for (int i = 0; i < words.length; i ++) {
            String s = words[i];
            int newCount = 0;
            if (count == 0) {
                newCount = s.length();
            }
            else {
                newCount = count + 1 + s.length();
            }
            if (newCount <= maxWidth) {
                line.add(s);
                count = newCount;
            }
            else {
                String newLine = getLine(line, count, maxWidth);
                res.add(newLine);
                line.clear();
                count = s.length();
                line.add(s);
            }
        }
        
        String newLine = getLastLine(line, maxWidth);
        res.add(newLine);
        
        
        return res;
    }
    private String getLastLine(List<String> line, int width) {
        StringBuilder sb = new StringBuilder();
        for (String word:line) {
            sb.append(word + " ");
        }
        sb.deleteCharAt(sb.length() - 1);
        while (sb.length() < width) {
            sb.append(" ");
        }
        return sb.toString();
    }
    private String getLine(List<String> line, int count, int width) {
        int numOfSpace = line.size() - 1;
        int addSpaceCount = width - count;
        String equalSpace = "";
        int bonusCount = 0;
        if (numOfSpace != 0) {
            int equalSpaceCount = addSpaceCount / numOfSpace;
            bonusCount = addSpaceCount % numOfSpace;
            for (int i = 0; i < equalSpaceCount; i ++) {
                equalSpace += " ";
            }
        }
        StringBuilder sb = new StringBuilder();
        int index = 0;
        for (String word:line) {
            sb.append(word);
            if (index < bonusCount) {
                sb.append(" " + equalSpace + " ");
            }
            else if (index != line.size() - 1) {
                sb.append(" " + equalSpace);
            }
            index ++;
        }
        while (sb.length() < width) {
            sb.append(" ");
        }
        return sb.toString();
    }
}
```