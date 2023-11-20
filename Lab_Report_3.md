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

- The fix to the was making the loop only loop for half the array length. Then, inside the for loop, we create a temporary variable that is equal to the index at i. We then swap the index at i to the last index and we change the last index to the index at i.

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
- Using the -iname command searches for the file or directory that has the specific name that you inputted and it ignores capitals or lowercase (case insensitive).
- This is useful because if you know the name of file/directory but you don't remember where there are capitals, you can use find -iname. It is case-insensitive.
- In the example, I used -iname and capitalized the name of a file in technical/911report and it returned the file I wanted to find. It ignored my capitalization.
- If there is no result, that means the file/directory that you were trying to search for doesnt exist.

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
- Using max depth limit the depth of searches by inputting the number of directories you want to find to descend into after the starting point. It used to recursively search for files and directories in a given directory and its subdirectories.
- It's good for searching quickly for something without having to go through all the subdirectories.
- In the example, I used -maxdepth 1 for directories and it resulted in the immediate directories of technical being printed because I went one level inside technical. 
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
- If you want to know what files or directories are empty, the -empty command is used to find empty files or directories. You use it to check for any empty directories or files.
- In the examples, I used the command to try to find empty files or directories inside technical, however, sinze there aren't any, there was no result.
- If there are empty files/directories, you can delete them to declutter because what's the use of having an empty file/directory if it's not going to be used.

```
find technical -type f -size +100k
technical/government/About_LSC/commission_report.txt
technical/government/About_LSC/State_Planning_Report.txt
technical/government/Env_Prot_Agen/multi102902.txt
technical/government/Env_Prot_Agen/ctm4-10.txt
technical/government/Env_Prot_Agen/bill.txt
technical/government/Env_Prot_Agen/tech_adden.txt
technical/government/Gen_Account_Office/d0269g.txt
technical/government/Gen_Account_Office/GovernmentAuditingStandards_yb2002ed.txt
technical/government/Gen_Account_Office/Sept27-2002_d02966.txt
technical/government/Gen_Account_Office/d01376g.txt
technical/government/Gen_Account_Office/Statements_Feb28-1997_volume.txt
technical/government/Gen_Account_Office/pe1019.txt
technical/government/Gen_Account_Office/gg96118.txt
technical/government/Gen_Account_Office/d01591sp.txt
technical/government/Gen_Account_Office/im814.txt
technical/government/Gen_Account_Office/ai9868.txt
technical/government/Gen_Account_Office/May1998_ai98068.txt
technical/government/Gen_Account_Office/d02701.txt
technical/biomed/1471-2105-3-2.txt
technical/911report/chapter-13.4.txt
technical/911report/chapter-13.5.txt
technical/911report/chapter-13.2.txt
technical/911report/chapter-13.3.txt
technical/911report/chapter-3.txt
technical/911report/chapter-1.txt
technical/911report/chapter-6.txt
technical/911report/chapter-7.txt
technical/911report/chapter-9.txt
technical/911report/chapter-12.txt
```
```
find technical -type d -size +1k
technical/government/Gen_Account_Office
technical/government/Media
technical/plos
technical/biomed
```
- The -size command is used to find files/directories that are greater or less than a certain size that you input.
- In the two examples, I used -size +100K to find files that were greater than 100 kilobytes. It then listed all the files inside technical that were greater than that size. It went through all the directories as well.
- This is useful for finding files/directories that are greater or less than a certain size. You can use this to find huge files or small files that you may want to delete (either it takes up too much space or it's useless).


**CITATION WEBSITES**
https://www.redhat.com/sysadmin/linux-find-command
https://helpdeskgeek.com/linux-tips/linux-find-command-with-examples/
