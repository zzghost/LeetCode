# Reverse Bits
Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).

Follow up:
If this function is called many times, how would you optimize it?

Related problem: [Reverse Integer](https://github.com/zzghost/leetcode/blob/master/007_Reverse_Integer.md)

## Solution
```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int rst = 0;
        for(int i = 0; i < 32; i++){
            rst += (n & 1);
            n = n >>> 1;
            if(i < 31)
                rst = rst << 1;
        }
        return rst;
    }
}
```
