# Crawler-Log-Folder

The Leetcode file system keeps a log each time some user performs a change folder operation.

The operations are described below:

"../" : Move to the parent folder of the current folder. (If you are already in the main folder, remain in the same folder).
"./" : Remain in the same folder.
"x/" : Move to the child folder named x (This folder is guaranteed to always exist).
You are given a list of strings logs where logs[i] is the operation performed by the user at the ith step.

The file system starts in the main folder, then the operations in logs are performed.

Return the minimum number of operations needed to go back to the main folder after the change folder operations.

Example 1:

Input: logs = ["d1/","d2/","../","d21/","./"]
Output: 2
Explanation: Use this change folder operation "../" 2 times and go back to the main folder.

Example 2:

Input: logs = ["d1/","d2/","./","d3/","../","d31/"]
Output: 3
Example 3:

Input: logs = ["d1/","../","../","../"]
Output: 0
 
Constraints:

1 <= logs.length <= 103
2 <= logs[i].length <= 10
logs[i] contains lowercase English letters, digits, '.', and '/'.
logs[i] follows the format described in the statement.
Folder names consist of lowercase English letters and digits.

# SOLUTION

# Intuition
There's no need in this approach if you solve specifically this problem, but what if you were asked to return actual path where user stopped?

We start in main folder, so initially our path stack is empty. We want to use stack because as soon as we find ../ we want to pop the last path we added to this stack
We iterate through logs and every time we face ../ we pop last element from stack (only if it's not empty, which tell us that we are already in main)
Every time we face not ../ and not ./ we add log to the stack as new path element.
At the end we want to return len of the stack because it's number of steps we need to return to main (pop every element from path with ../)
# Coding
Initialize an empty list paths_stack to keep track of the current directory path.
Iterate through each log entry in the logs list:
If the log is ../, check if paths_stack is not empty and pop last element
If the log isn't ../ or ./ then add new path element to paths_stack
Return length of the path_stack after perfoming all operations

# Complexity Analysis
-Time complexity: O(n), since we iterate through whole array logs
-Space complexity: O(n), since we use paths_stack which can be of size n in worst case

 # JAVA CODE

 class Solution {
 
    public int minOperations(String[] logs) {

         Stack<String> paths_stack = new Stack<>();

        for (String log : logs) {
        
            if (log.equals("../")) {
            
                if (!paths_stack.isEmpty()) {
                
                    paths_stack.pop();
                }
            } else if (!log.equals("./")) {
            
                paths_stack.push(log);
            }
        }

        return paths_stack.size();
        
    }
}
