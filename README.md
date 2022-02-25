# Report for assignment 3
## Project
Name: Gson \
URL: [https://github.com/DD2480-group4-22/gson](https://github.com/DD2480-group4-22/gson) \
Gson is a library for Java that can be used to convert Java objects into their JSON representation and JSON strings into their Java object equivalent.
## Onboarding experience
1. How easily can you build the project? Briefly describe if everything worked as documented or not:
  (a) Did you have to install a lot of additional tools to build the software?
    Building the project wasn’t difficult. To build the project either Maven or Gradle has to be installed. The group has used Maven before, it is well documented and easy to use, So therefore we decided to use it.

  (b) Were those tools well documented?
    The project is well documented, but the use of maven isn’t perfectly documented, though using maven is very standardized and well documented so it is easy to know what commands to run to work with the project.

  (c) Were other components installed automatically by the build script?
    All the dependencies for the project is downloaded when you run Maven.

  (d) Did the build conclude automatically without errors?
    Some of us had a problem where there would be an error when building the project, but it was resolved by using an older version of java.

  (e) How well do examples and tests run on your system(s)?
    Building and running the test went smoothly and no unexpected errors occurred. First time it took approximately 2 minutes to build and run the test which seems reasonable, running the test after building took approximately 30 seconds.

2. Do you plan to continue or choose another project?
  Since everything went good for all of us running the project we continued on it.

## Complexity
The group used Lizard for calculating the complexity of the code. It checks both the number of lines in the code (but excluding lines with comments) and the cyclomatic complexity of the code. The results are very clear if you’re looking for the most complex functions since it gives a table of the most complex ones (CC > 15, length > 1000, lines of code > 1 000 000) at the end. You can use the -s flag to sort the most complex ones.

Each group member identified two methods with high complexity (in total 10 methods):
1. **nextDouble** (/gson/src/main/java/com/google/gson/stream/JsonReader.java) \
NLOC: 31 \
CCN: 12 \
\
The method is not very long, but still has a very high cyclomatic complexity. The purpose of the method is to return the double value of the next token in the stream. It contains many if-statements depending on what the next token is and that is what makes the method complex. There is some code duplication between this method and similar methods like nextLong. With refactoring the complexity could probably be lowered for these methods. Exceptions are handled within the method and I think they are taken into account by Lizard. The method has clear documentation in the form of JavaDoc, but it does not document all the different branches.

2. **skipUnquotedValue** (/gson/src/main/java/com/google/gson/stream/JsonReader.java) \
NLOC: 29 \
CCN: 19 \
\
The method is not very long, but still has a very high cyclomatic complexity. The purpose of the method is to skip values in the stream that is not quoted. There are different rules for what it should do if the next character is a certain type of character like a parenthesis or a colon. Since the method has to follow the rules and the rules are a bit complex, then the method becomes complex too. Exceptions are handled by another method that is called for certain cases. If the exception handling would have been done in the method and we think of exceptions as another possible branch, then the CC would probably increase. Most other methods have JavaDoc, but this method does not have any documentation.

3. **NextLong** (/gson/src/main/java/com/google/gson/stream/JsonReader.java) \
NLOC: 40 \
CCN: 11 \
\
The method is considered to have a very high CC but it does not have so many lines of code. It is built up with if-statements which gives it the high complexity. he NextLong method returns the value of the next token, and if the token is a string the method will parse it as a long, if it is a numeric value that cannot be represented with long an exception will be thrown. The method has clear documentation in the form of JavaDoc, but it does not document all the different branches.

4. **NextInt** (/gson/src/main/java/com/google/gson/stream/JsonReader.java) \
NLOC: 45 \
CCN: 12 \
\
The method is considered to have a very high CC but it does not have so many lines of code. The nextInt method also returns the value of the next token and if it is a string the method will parse it to an int. Exception is thrown similarly as in NextLong when the next token's numeric value cant be represented as an int an exception is thrown. The method has clear documentation in the form of JavaDoc, but it does not document all the different branches.

5. **doPeek** (/gson/src/main/java/com/google/gson/stream/JsonReader.java) \
NLOC: 125 \
CCN: 41 \
\
This is the "main" method of the JsonReader. It checks the current token of the Json-file to see what it is and what it should be turned into. Since there are many different types of objects the Json could contain this method is naturally very complex.

6. **parse** (/gson/src/main/java/com/google/gson/internal/bind/util/ISO8601Utils.java) \
NLOC: 113 \
CCN: 32 \
\
Function for parsing and formatting dates in ISO8601 format. It has to check for many different types of date-formats which leads to the high complexity of the function.

7. **readEscapeCharacter** (/gson/gson/src/main/java/com/google/gson/stream/JsonReader.java) \
NLOC: 48 \
CCN: 23 \
\
The method has one switch-case with 11 cases, in one case for-statement and else-if-statements. Few lines compared to the high cyclomatic complexity mainly because of the switch-case statement. The method unescapes characters followed by backslash as well as the character identified by the character. The method throws IOException and throws in branches syntaxErrors and NumberFormatExpression. Throwing exceptions in additional branches creates a higher CCN, noted by lizard as well, but can through the exception message provide more details about what went wrong. The exception itself does however not change the CCN using the lizard tool but the branch it is placed in does.
The documentation of the method is clear about the different outcomes of the branches, if you are familiar with the terminology “unescapes”.


8. **peek** (/gson/gson/src/main/java/com/google/gson/stream/JsonReader.java) \
NLOC: 37 \
CCN: 19 \
\
The method has one if-statement and then switch case with 17 cases. Not very long code but high complexity because of the switch case with each case counting as one node.
The purpose of the method peek() is to return the type of the next JsonToken without consuming it. Since there are many cases to consider it is related to the high CCN. \
\
Exceptions with an if-statement would make a difference in the CCN and the amount of lines in the code, since additional edges are added compared to nodes in the flow-graph when creating the if-statements. However the specific throw of an exception does not change the CCN, as an exit, using the lizard tool. The method throws IOException and the default in the switch-case throws AssertionError(). There was no exception to be taken into account, except for the throw of AssertionError() in the manual counting of CCN. \
\
The documentation for the method is one short line but is enough to say what the method does and together with the documentations of the class JsonReader() the different cases are clear. I would not however say that all outcomes are clear, since not all cases have return statements and thereby fall-through and another values is returned in a latter case. I would not say that the documentation provides information to make it clear why the code does so.

9. **nextNonWhitespace** (/gson/gson/src/main/java/com/google/gson/stream/JsonReader.java) \
NLOC: 68 \
CCN: 16 \
\
Function returns the position of the next character that isn’t a whitespace or part of a comment. It is complex because it contains a mixture of switch cases and if & else statements that handle the different cases for this method, such as if the character is part of a comment or is a whitespace. The method seems decently sized, but the amount of conditional statements makes it very packed. However, the size isn’t the contributing factor for why it is complex. The method has quite a bit of documentation, but it doesn’t explain completely the branching paths it can take. This function can throw exceptions, but the program I used to check for cyclomatic complexity doesn’t seem to be taking into account if the code throws an exception.

10. **isLiteral** (/gson/gson/src/main/java/com/google/gson/stream/JsonReader.java) \
NLOC: 24 \
CCN: 17 \
\
Function checks if a character sent as a parameter is a literal or not. It is complex because it contains a lot of switch cases with fallthrough. I got the same cyclomatic complexity when I calculated by hand as I got from the Lizard tool. The method is pretty short, but the complexity is very high. So I don’t think a large LOC means more complex code. The method has no documentation, but by looking at the code it is clear what it does. Exception handling is done by another function, though if it was included in the code it should’ve increased the cyclomatic complexity, as it can be seen as a branch the program can take.


### Counted by hand

Every group member also counted the complexity of one of their choosen methods by hand (in total 5 methods):
1. **skipUnquotedValue**: CCN =  #decisions - #exitPoints + 2 = 18 - 3 + 2 = 17.
2. **nextLong**: CCN = E - N + 2 = 15 - 10 + 2 = 7
3. **doPeek**: CCN = 43
4. **peek**: CCN = E - N + 2 = 40 - 23 + 2 = 19
5. **isLiteral**: CCN = (#case + #fallthroughs) - #states + 2 = (17+15) - 17 + 2 = 17

* Add comment regarding if the values match Lizard or not

## Refactoring
We found five functions with high complexity that all had code duplication between them. These methods are in JsonReader.java and are **peek**(CCN 19), **nextdouble**(CCN 12), **nextInt**(CCN 12), **nextLong**(CCN 11) and **nextString**(CCN 8).

This is the code that is duplicated in all those methods:
```
int p = peeked;
if (p == PEEKED_NONE) {
      p = doPeek();
}
```

and we could refactor all the five methods by making this into its own method
```
private int assignP() {
      int p = peeked;
      if (p == PEEKED_NONE) {
           p = doPeek();
      }
      return p;
}
```
Then in the five methods we would only have to write
```
int p = assignP();
```
This would remove a decision from the methods, which would lower the CCN. One possible drawback is that it might be hard to understand what assignP() means and then you would have to go that method and read the documentation.


## Coverage
### Tools
The tool we used for coverage measurement was OpenClover. It was possible to use it with Maven and since we already used Maven for the project, it was rather easy to integrate it with the build environment. It was well documented and the only thing we had to do was to add this plugin to the pom.xml file:
```
<plugin>
  <groupId>org.openclover</groupId>
  <artifactId>clover-maven-plugin</artifactId>
  <version>4.4.1</version>     
</plugin>
```
Then when running this command OpenClover generated HTML files that among other things displayed the coverage of all methods:
```
mvn clean clover:setup test clover:aggregate clover:clover
```
### Your own coverage tool
Show a patch (or link to a branch) that shows the instrumented code to
gather coverage measurements.
The patch is probably too long to be copied here, so please add
the git command that is used to obtain the patch instead:
git diff ...
What kinds of constructs does your tool support, and how accurate is
its output?

Each group member made their own coverage tool for one method
### Anna

### Elsa
Made a coverage tool for doPeek in JsonReader.java in the branch branch_coverage_elsa. The code can be found in [JsonReader.java](https://github.com/DD2480-group4-22/gson/blob/branch_coverage_elsa/gson/src/main/java/com/google/gson/stream/JsonReader.java) (the method doPeek() and [JsonReaderTest.java](https://github.com/DD2480-group4-22/gson/blob/branch_coverage_elsa/gson/src/test/java/com/google/gson/stream/JsonReaderTest.java) (at the end of the file, the @AfterClass). Works by setting a value in a boolean array to true if the branch is taken. Read Oskar's text for more info.
### Jacob

### Nelly

### Oskar
I made a coverage tool for the method skipUnquotedValue in JsonReader.java. The code can be found in the branch **branch_coverage_oskar** at this link: [https://github.com/DD2480-group4-22/gson/tree/branch_coverage_oskar](https://github.com/DD2480-group4-22/gson/tree/branch_coverage_oskar)

First I gave every branch of the method a unique ID. Then I made a boolean array with one element for each branch. In the method if a branch was reached its respective element in the array was set to true. Then in the JavaReaderTest class the results are printed out after all tests have been run. To make sure the printCoverage method was run after all tests I used the @AfterClass annotation. This annotation was not available for JUnit3 which the test class used, so I had to convert everything to JUnit4 in order to make it work.

### Evaluation
1. How detailed is your coverage measurement?
2. What are the limitations of your own tool?
3. Are the results of your tool consistent with existing coverage tools?
## Coverage improvement
Show the comments that describe the requirements for the coverage.
Report of old coverage: [link]
Report of new coverage: [link]

Below follows the tests cases each group member added and the changes in coverage it made

### Anna
1. Added test for hashtag in isLiteral in JsonReaderTest.java
  ```
public void testHashtag() throws IOException {
    JsonReader reader = new JsonReader(reader("[true#true]"));
    reader.beginArray();
    try {
      assertEquals(JsonToken.BOOLEAN, reader.peek());
      reader.nextBoolean();
      reader.nextBoolean();
      fail();
    } catch (IOException expected) {
    }
  }
```
**Coverage before test:**
![](/img/AnnaCoverageBefore1.png)

**Coverage after test:**
![](/img/AnnaCoverageAfter1.png)

2. 
Added test for equals in isLiteral in JsonReaderTest.java

```
  public void testEqual() throws IOException {
    JsonReader reader = new JsonReader(reader("[true=true]"));
    reader.beginArray();
    try {
      assertEquals(JsonToken.BOOLEAN, reader.peek());
      reader.nextBoolean();
      reader.nextBoolean();
      fail();
    } catch (IOException expected) {
    }
  }
  ```

**Coverage before test:**
![](/img/AnnaCoverageBefore2.png)

**Coverage after test:**
![](/img/AnnaCoverageAfter2.png)

**Coverage for isLiteral**
Coverage of the method isLiteral before any added test were 71.4% and after the two added test it is 81%.
![](/img/AnnaIsLiteralCoverAfter.png)
![](/img/AnnaIsLiteralCoverageBefore.png)


### Elsa
Both tests are in the same file. The new tests are at the end of the file.\
[**Coverage before test.**](https://github.com/DD2480-group4-22/gson/blob/ca2ed748ba6e31c4a319ea6f2d2dc7048021f0a0/gson/src/test/java/com/google/gson/internal/bind/util/ISO8601UtilsTest.java) \
[**Coverage after test.**](https://github.com/DD2480-group4-22/gson/blob/master/gson/src/test/java/com/google/gson/internal/bind/util/ISO8601UtilsTest.java)

1. In **ISO8601Utils.java**:\
Added test for missing time-zones in ISO8601UtilsTest.java:
```
 @Test
public void testDateHasNoTimeZone() throws ParseException {
        final String dateStr = "2018-06-25T61:60:62";
        assertThrows(ParseException.class, new ThrowingRunnable() {
          @Override
          public void run() throws Throwable {
            ISO8601Utils.parse(dateStr, new ParsePosition(0));
          }
        });
}
```

**Coverage before test:**
![](/img/Coverage_Elsa_before_1.png)

**Coverage after test:**
![](/img/Coverage_Elsa_after_1.png)

2. In **ISO8601Utils.java**:\
Added test for invalid time-zone indicator in ISO8601UtilsTest.java:
```
@Test
public void testDateInvalidTimeZoneFormat() throws ParseException {
    final String dateStr = "2018-06-25T61:60:62*03:00";
    assertThrows(ParseException.class, new ThrowingRunnable() {
         @Override
         public void run() throws Throwable {
           ISO8601Utils.parse(dateStr, new ParsePosition(0));
         }
   });
}
```
**Coverage before test:**
![](/img/Coverage_Elsa_before_2.1.png)
![](/img/Coverage_Elsa_before_2.2.png)

**Coverage after test:**
![](/img/Coverage_Elsa_after_2.1.png)
![](/img/Coverage_Elsa_after_2.2.png)

### Jacob

### Nelly

### Oskar
I added five new test cases for skipUnquotedValue in (/gson/src/main/java/com/google/gson/stream/JsonReader.java). Each one of the tests covers a new branch that was not covered before.

1.
```
@Test
  public void testSkipUnquotedSlash() throws IOException {
    JsonReader reader = new JsonReader(reader("{" + "x" + "/"));
    reader.setLenient(true);
    assertEquals(JsonToken.BEGIN_OBJECT, reader.peek());
    reader.beginObject();
    reader.skipValue();
  }
```
2.
```
  @Test
  public void testSkipUnquotedBackslash() throws IOException {
    JsonReader reader = new JsonReader(reader("{" + "x" + "\\"));
    reader.setLenient(true);
    assertEquals(JsonToken.BEGIN_OBJECT, reader.peek());
    reader.beginObject();
    reader.skipValue();
  }
```
3.
```
  @Test
  public void testSkipUnquotedSemicolon() throws IOException {
    JsonReader reader = new JsonReader(reader("[" + "x" + ";"));
    reader.setLenient(true);
    assertEquals(JsonToken.BEGIN_ARRAY, reader.peek());
    reader.beginArray();
    reader.skipValue();
  }
```
4.
```
  @Test
  public void testSkipUnquotedHashtag() throws IOException {
    JsonReader reader = new JsonReader(reader("{" + "x" + "#"));
    reader.setLenient(true);
    assertEquals(JsonToken.BEGIN_OBJECT, reader.peek());
    reader.beginObject();
    reader.skipValue();
  }
```
5.
```
  @Test
  public void testSkipUnquotedEquals() throws IOException {
    JsonReader reader = new JsonReader(reader("[" + "x" + "="));
    reader.setLenient(true);
    assertEquals(JsonToken.BEGIN_ARRAY, reader.peek());
    reader.beginArray();
    reader.skipValue();
  }
```
In the image below you can see the difference calculated by my own coverage tool between before and after adding the tests:
![](/img/oskarToolBeforeAfter.png)

Before 6/20 branches are covered and after 11/20 branches are covered.

According to OpenClover the branch coverage went from 46,4% to 67,9% after adding the tests, which can be seen in the image below:

![](/img/OskarCoverageClover.png)

Then in this image you can see which part of the method that gets covered by the new tests:

![](/img/OskarCoverageBeforeAfter.png)


## Self-assessment: Way of working
According to the Essence standard of way-of-working our team is in the "working well" phase. We have established good communication and praxis of how to do the work that flows naturally. When assigned to task each team member is available to help one another if necessary and work flow is even. We have developed a understanding between each other and in the beginning we were all strangers but with regular communication we now know how we work and our strengths. Continue to work as we currently do with open communication and helping each other is the plan to move forward.

## Overall experience
During the course of this project we learnt a lot. We got the chance to work on a larger code base and experience the challenges of it. We also got a better idea on how it can be to contribute to an open source project. This is probably the main take-away from the project and now we have the knowledge to be able to contribute to more open source projects in the future. Apart from that we also learnt about cyclomatic complexity, branch coverage and refactoring.
## P+
What did we do for P+
