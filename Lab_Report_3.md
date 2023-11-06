**LAB REPORT 3**
**Kwae Htoo, A17327141**

**PART 1**

This is the buggy code block I chose (reverseInPlace method):
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

A failure-inducing input for the buggy program, as a JUnit test and any associated code:
```
 @Test
  public void testReverseInPlaceB() {
    int[] input = {1,2,3,4,5};
    ArrayExamples.reverseInPlace(input);
    int[] expected = {5,4,3,2,1};
    assertArrayEquals(expected, input);
  }
```

An input that doesn’t induce a failure, as a JUnit test and any associated code:
```
@Test 
  public void testReverseinPlaceC() {
    int[] input = {2,2,2};
    ArrayExamples.reverseInPlace(input);
    int[] expected = {2,2,2};
    assertArrayEquals(expected, input);
  }
```

The symptom, as the output of running the tests:
<img width="647" alt="Screen Shot 2023-11-05 at 4 35 21 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/9a3c9521-94c6-498b-819f-a2531c251bb7">

<img width="442" alt="Screen Shot 2023-11-05 at 4 35 47 PM" src="https://github.com/verylemons/cse15l-lab-reports/assets/116234889/af4fb472-547e-4b88-8898-3fe4fc4f6b65">

The bug, as the before-and-after code change required to fix it:

Before Code:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

After Code (fixed):
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```

**PART 2**
- The command that I will choose is **find**.

Alternative ways:

```
find technical -iname "CHAPTER-1.txt"
technical/911report/chapter-1.txt
```
```
find technical -iname "GovERNMENT"
technical/government
```
- This is useful because if you know the name of file/directory but you don't remember where there are capitals, you can use find -iname. It is case-insensitive.

```
find technical -maxdepth 1 -type d
technical
technical/government
technical/plos
technical/biomed
technical/911report
```
```
find technical/government -maxdepth 1 -type f
// nothing gets printed because because if you go 1 depth into technical/government, there is no files.
```
- This is useful because it limits how deep you want to go inside a directory. When there a directories inside directories, you can use
  -maxdepth to limit how many times you want traverse through directories inside another directory.

```
find technical -type d -empty
// nothing gets printed out because none of the directories are empty
```
```
find technical -type f -empty
// nothing gets printed out because no files within the directories inside of technical are empty
```
- This is useful for finding empty files or directories. If there are empty files/directories, you can delete them to declutter because what's the use of having an empty file/directory if it's not going to be used.

  


