# Lab report 2

## Part 1

![First word added](First_word_added.png)
The main method in my code that is called to add these new strings is the `if (url.getPath().contains("/add-message"))` portion of my code.
This part will basically see if the URI I put in includes the /add-messages part of the URI that we determined we needed for this function to work.
Afterwards it breaks up the input by taking what comes after `?s=` and putting it into a string array. Then all I did was add some code that 
takes the new added word, and then transfers it to a string ArrayList to then be put onto the homepage. Specifically in this request, 
because `?s=` is followed by `Hola`, I then add Hola into storedWords.

![Second word added](2nd_word.png)
The main method again is the `if (url.getPath().contains("/add-message"))` and everything else follows the exact same process as before. The only
difference this time around is that instead of Hola, a `Hello` is in front of the `?s=` portion of the URI. This means `paraneters[1]` will be Hello,
and thus will be added to storedWords.

![Home page](home.png)

## Part 2
**Bug input:**
```Java
@Test
  public void testReversedLong() {
    int[] input = {1, 2, 3, 4, 5, 6, 7};
    int[] reversed = {7, 6, 5, 4, 3, 2, 1};
    assertArrayEquals(reversed, ArrayExamples.reversed(input));
  }
 ```

**Input that doesn't bug:**
```Java
@Test
  public void testReversed() {
    int[] input1 = { };
    assertArrayEquals(new int[]{ }, ArrayExamples.reversed(input1));
  }
 ```

**Symptoms seen in cmd:**
```Java
$ java -cp ".;lib/junit-4.13.2.jar;lib/hamcrest-core-1.3.jar" org.junit.runner.JUnitCore ArrayTests
JUnit version 4.13.2
...E
Time: 0.005
There was 1 failure:
1) testReversedLong(ArrayTests)
arrays first differed at element [0]; expected:<7> but was:<0>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReversedLong(ArrayTests.java:23)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<7> but was:<0>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more

FAILURES!!!
Tests run: 3,  Failures: 1
```

**Fixed code in ArrayExamples:**
Before:
```Java
  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
 ```

After:
```Java
  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = arr.clone();
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
 ```

This fixes the code because prior to this, what was happening was newArray was being created as an empty array that was the same length as the input array.
Then from this array, it was copying each value backwards into the output array to reverse it. However, this did not work for any array that either wasn't empty
or full of 0's because every iteration over the empty array would just put 0 in whatever index it was being sent to. In order to fix this, I cloned the first array 
that was to be reversed, then it could properly be iterated over backwards, thus fixing the method.

## Part 3

One thing I learned this week was how the JUnit tests actually worked. I had only really learned about them this quarter thanks to CSE 12, but I had no idea how they
really worked or what they even were. However, Lab 3 helped me gain a newfound understanding for them, and I now feel confident that I can use them in the terminal, and don't need to be guided around like a baby through an IDE to use it.
