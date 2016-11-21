# 71 Simplify Path – Medium


### Problem:



Given an absolute path for a file (Unix-style), simplify it.

For example,
path = "/home/", => "/home"
path = "/a/./b/../../c/", => "/c"


### Thoughts:


This is a good example to use stack. Split input string by “/”, then iterate over the string array.

If it’s empty or “.”, don’t do anything. If it’s “..”, pop one element. Otherwise, put the part into the stack.


### Solutions:



```java
public class Solution {
    public String simplifyPath(String path) {
        String[] parts = path.split("/");
        Stack<String> stack = new Stack<String>();
        for (int i = 0; i < parts.length; i ++){
            if (parts[i].equals("") || parts[i].equals(".")){
                continue;
            }
            else if (parts[i].equals("..")){
                if (!stack.empty()){
                    stack.pop();
                }
            }
            else{
                stack.push(parts[i]);
            }
         }//for
        String res = "";
        if (stack.empty()){
            return "/";
        }
        else{
            while(!stack.empty()){
                res = "/" + stack.pop() + res;
            }
            return res;
        }
    }
}
```