# 271. Product of Array Except Self
https://leetcode.com/problems/encode-and-decode-strings/description/

```
public class Codec {
//escape
//if "//:" in a word, it is regraded as an original word instead of escaping char
    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        StringBuilder encodeStr = new StringBuilder();
        for (String s : strs) {
            encodeStr.append(s.replace("/", "//")).append("/:");
        }
        return encodeStr.toString();
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String s) {
        List<String> decodedStr = new ArrayList<>();
        StringBuilder curStr = new StringBuilder();
        int i = 0;
        while (i<s.length()) {
            if (i+1 <s.length() && s.charAt(i) == '/' && s.charAt(i+1) == ':') {
                decodedStr.add(curStr.toString());
                curStr = new StringBuilder();
                i+=2;

            } else if (i+1<s.length() && s.charAt(i) == '/' && s.charAt(i+1)=='/') {
                curStr.append('/');
                i+=2;
            } else {
                curStr.append(s.charAt(i));
                i++;
            }
        }

        return decodedStr;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```

key:
1.escaping转义
2.use '/:' as escaping chars to break strings
3.if '/' is in a world we repaced it as '//' in case there is '/:' in a string