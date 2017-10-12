# Student Attendance Record
## Description
You are given a string representing an attendance record for a student. The record only contains the following three characters:  

'A' : Absent.  
'L' : Late.  
'P' : Present.  
A student could be rewarded if his attendance record doesn't contain more than one 'A' (absent) or more than two continuous 'L' (late).  

You need to return whether the student could be rewarded according to his attendance record.  

**Example 1:**
```
Input: "PPALLP"
Output: True
```
**Example 2:**
```
Input: "PPALLL"
Output: False
```

## Solution
**Complexity: Time O(n), Space O(n).**
```java
public boolean checkRecord(String s) {
    int countA = 0, countL = 0;
    char[] alpha = s.toCharArray();
    for(int i = 0; i < s.length(); i++){
        if(alpha[i] == 'A'){
            countA++;
            if(countA > 1)
                return false;
        }
        if(alpha[i] == 'L'){
            countL++;
            if(countL > 2)
                return false;
        }
        else{
            countL = 0;
        }
    }
    return true;
}
```
