**LAB REPORT 3**
**Kwae Htoo, A17327141**

**PART 1**

*A failure-inducing input for the buggy program, as a JUnit test and any associated code*
    int[] input1 = {1, 2, 3, 4, 5};
    int[] output1 = {5, 4, 3, 2, 1};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(output1, input1);

*An input that doesn’t induce a failure, as a JUnit test and any associated code*
    int[] input2 = {2,2};
    int[] output2 = {2,2};
    ArrayExamples.reverseInPlace(input2);
    assertArrayEquals(output2, input2);

static void reverseInPlace(int[] arr) {
    int temp = 0;
    for(int i = 0; i < arr.length/2; i += 1) {
      temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
