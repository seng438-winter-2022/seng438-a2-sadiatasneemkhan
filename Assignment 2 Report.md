**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report \#2 – Requirements-Based Test Generation**

| Group \:  35     |            |
|-------------------|------------|
| Student Names:    |    UCID    |
| Luis Sulbaran     | 30090906   |
| Adam Abouelhassan | 30087777   |
| Jaxson Waterstreet| 30095706   |  
| Sadia Khan        | 30090271   |

# 1 Introduction

The goal of this lab was to learn how to design and implement proper unit tests using the testing strategies learned in lectures. Black-box testing was the main focus, as we gained knowledge about he function through its JavaDoc, since we did not have access to the implementation of the methods. This lab utilized Junit on Eclipse to test the various methods of class Range and DataUtilities. 

# 2 Detailed description of unit test strategy

The testing strategies we used to design our test cases followed the black-box design techniques of equivalence class testing and boundary value testing. 

## Equivalence Class Testing (ECT)
Through equivalence class testing, we were able to divide possible method inputs into “partitions”, which then allowed us to separate any valid and invalid inputs. In each test case, we followed the ECT principles by deciding how many independent variables we will have to work with. We then decided how many distinct partitions were needed to cover all possible edge cases. Following this style, we were able to then create tests cases using acceptable values from each partition, and were able to distinguish any redundant cases and/or add more tests to problems that came up. For example, when working with the contains() method in the Range class, we used the 2 independent variables we were working with to come up with 3 distinct partitions. For a range of (-100, 200), any invalid inputs would appear from the range -inf to -100 and 200 to +inf. All valid inputs would appear from any range -100 to 200. We were then able to break down our partitions even further by using BVT which I will discuss in the following section.

### Range contain() method example:

	1. Decide the number of independent variables: 2.
	2. How many distinct partitions? 3.
	3. Number of test cases based on criteria? 3.
	4. Create tests using acceptable values assigned from each partition

![RangeEx1](https://user-images.githubusercontent.com/81999006/153535520-dbb6cd04-d2eb-4052-bc2e-e0998c36b2a0.png)

## Boundary Value Testing (BVT)
Boundary value testing was another testing technique that we performed which allowed us to process inputs at or near the boundaries of our equivalence classes. BVT was crucial in our testing to develop more accurate test cases where we could discover any hidden inputs that could have possibly failed our tests. A lot of times, test developers run into bugs when the methods are tested with values that lie exactly on or close to a boundary. BVT allows us to solve this problem, which is why we followed this testing method to cover all sides of our boundary partitions. We will continue by using the example that was mentioned above to better understand how it was developed on from the ECT method. As mentioned before and seen in our image, our range extended from -100.0 to 200.0. Using this range, we were able to test all possible bugs for this method by covering all boundaries with 7 possible inputs as shown in the image below.

![RangeEx2](https://user-images.githubusercontent.com/81999006/153535522-668af948-a74f-4b14-809c-e2abd1e673ea.png)

## Discussion on Mocking

Since some of our methods use interfaces such as Values2D, we cannot test them without mocking. Mocking will allow us to separate the method we are testing from any external objects that it uses. By creating a mock object, we have a dummy implementation for the interface. This benefit of mocking allows us to truly test only a single component, since it isolates the function that is being tested from its dependencies. A drawback of mocking with black-box testing we faced was not being able to see the source code, thus not knowing how the interface was being used and what limitations the interface objects have. 

# 3 Test cases developed

## RangeTest

## tests for expandToInclude() 

test_expandToInclude_withinRange()
- Covers the inputs for values that are within the provided range
- NOM: a nominal value

test_expandToInclude_outsideUpperRange()
- Covers the inputs for values that are outside of the upper bound of the provided range
- AUB : value just above upper bound

test_expandToInclude_outsideLowerRange()
- Covers the inputs for values that are outside of the lower bound of the provided range 
- BLB: value below lower bound

test_expandToInclude_lowerBoundary()
- Input covers the value on the lower boundary (LB)

test_expandToInclude_upperBoundary()
- Input covers the value on the upper boundary (UB)

Testing strategy: Using ECT, split into 3 partitionss which are (-inf, lower), (lower, upper) and (upper, +inf). Using BVT, the upper and lower bound values were also covered. NOM, AUB, BLB, LB, UB were all covered within these tests. Also, BUB and ALB inputs were covered through the within-range ECT.

## tests for getLowerBound() 

test_getLowerBound_negBound()
- Covers ranges with any negative lower bound

test_getLowerBound_posBound()
- Covers ranges with any positive lower bound

## tests for contains() 

test_contains_withinRange()
- Tests for values contained within the specified range

test_contains_upperBound()
- Tests for values that are exactly on the upper bound of the specified range

test_contains_lowerBound()
- Tests for values that are exactly on the lower bound of the specified range

test_contains_outsideLowerRange()
- Tests for values just outside of the lower bound of the specified range

test_contains_outsideUpperRange()
- Tests for values just outside of the upper bound of the specified range

test_contains_insideLowerRange()
- Tests for values contained just below the lower bound of the specified range

test_contains_insideUpperRange()
- Tests for values contained just below the upper bound of the specified range

Testing Strategy: Split up range into 3 different partitions using ECT which were (-inf, lower), (lower, upper) and (upper, +inf). Also used the BVT to expand our testing and cover all ranges to include BLB, LB, ALB, NOM, BUB, UB, and AUB.

## tests for getLength() 

test_getLength_negPos()
- Tests for the length of a range with negative lower bound and positive upper bound

test_getLength_negNeg()
- Tests for the length of a range with negative lower bound and negative upper bound

test_getLength_posPos()
- Tests for the length of a range with positive lower bound and positive upper bound

test_getLength_bigNegPos()
- Tests for the length of a range with a massive negative lower bound and massive positive upper bound

test_getLength_sameBounds()
- Tests for the length of a range with the same lower and upper bound

Testing Strategy: Using ECT, covered all types of inputs using various partitions. These inputs were, (+val, -val), (+val, +val), (-val, -val), (big +val, big -val), and (0,0).

## tests for getCentralValue() 

test_getCentralValue_negAndPosRange()
- Tests for the central value of a range with a negative lower bound and positive upper bound

test_getCentralValue_negRange()
- Tests for the central value of a range with a negative lower bound and negative upper bound

test_getCentralValue_posRange()
- Tests for the central value of a range with a positive lower bound and positive upper bound

test_getCentralValue_zeroRange()
- Tests for the central value of a range with the same lower bound and upper bound

Testing Strategy: Using ECT to cover partitions using different types of inputs (+val, -val), (+val, +val), (-val, -val), and using 0 as the central value (same lower
and upper bound).

## DataUtilitiesTest

## tests for calculateColumnTotal() 

test_calculateColumnTotal_posDoubleNum() 
- Tests for the summation of positive double numbers withing a column

test_calculateColumnTotal_negDoubleNum() 
- Tests for the summation of negative double numbers withing a column

test_calculateColumnTotal_posIntNum() 
- Tests for the summation of positive integer numbers withing a column

test_calculateColumnTotal_negIntNum() 
- Tests for the summation of negative integer numbers withing a column

Testing strategy: Using mocking, mock objects of Value2D were created in order to test the function independently with no dependencies.

## tests for equal() 

test_equal_normalCase()
- Tests two normal equal arrays
	
test_equal_notEqual()
- Tests two normal not equal arrays

test_equal_differentDimensions()
- Tests arrays with different dimensions
	
test_equal_bothNull()
- Tests the equality of two null arrays

test_equal_oneNull()
- Tests a null array with a normal one

test_equal_infValue()
- Tests two equal arrays containing infinite values

test_equal_nanValue()
- Tests two equal arrays containing NaN values

## tests for clone() 

test_clone_declare()
- Clones the array into an array that is being declared
	
test_clone_reassign()
- Reassigns an array value by cloning into it

test_clone_increaseDimensions()	
- Clones an array with greater dimensions 3x3 into an array with smaller dimensions 2x2

## tests for createNumberArray() 

test_createNumberArray_test()
- Test array of size 2

test_createNumberArray_bigNums()
- Test array of size 2 with very big values

test_createNumberArray_bigNegativeNums()
- Test array of size 2 with very negative values

test_createNumberArray_millionArray()
- Test array of size 1000000

test_createNumberArray_nullArray()
- Test null array

test_createNumberArray_testNullValue()
- Test array with a null value

## tests for createNumberArray2D() 

test_createNumberArray2D_test()
- Tests an array of size 2x2

test_createNumberArray2D_bigNums()
- Tests an array of size 2x2 with very large values

test_createNumberArray2D_bigNegativeNums()
- Tests an array of size 2x2 with very negative values

test_createNumberArray2D_millionArray()
- Tests an array of size 1000x1000

test_createNumberArray2D_nullArray()
- Tests a null array

test_createNumberArray2D_testNullValue()
- Tests an array with a null value

# 4 How the team work/effort was divided and managed

Since the lab required 10 methods to be tested, each team member was responsible for writing unit tests for 2-3 methods. After all the test cases had been completed, all the members gathered for a meeting and discussed each test case individually to see if they included all the requirements. This also allowed us to also learn from each other about unit testing, as we shared the thought process we conducted while designing our own test cases. For the lab report, all the members read through each required section and noted down short, brief notes that would be expanded on later in the report. Then we split the report sections so each member had a fair share of work. Before submitting, the group gathered again to review the report and be certain that all the lab requirements had been met.

# 5 Difficulties encountered, challenges overcome, and lessons learned

During this second lab, the majority of our group's problems came not from the content but other sources. No one in our group had much experience with Eclipse, so we had to work as a group to navigate our way through this unfamiliar IDE. Also we had a few difficulties handling the sheer volume of files involved while setting up the assignment. Both these challenges were overcome by communicating as a group and not being afraid to ask for help if stuck at any point. 

# 6 Comments/feedback on the lab itself

This lab was a useful and functional exercise for us, as it grew our familiarity with JUnit tests, mocking and Eclipse. The lab forced us to think of possible edge cases where the specified methods could fail, which expanded our knowledge on how to approach JUnit testing. Moving forward, I think this lab helped us learn how to properly test methods using JUnit tests and mocking. Throughout the lab we found a couple cases where the created JUnit tests would fail, the failed tests indicated bugs in the method code which should be fixed eventually.

