**LAB REPORT 3**
**Kwae Htoo, A17327141**

**PART 1**

This is the buggy code block I chose:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
