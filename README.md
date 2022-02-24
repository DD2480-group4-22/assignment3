# Report for assignment 3
## Project
Name: Gson \
URL: [https://github.com/DD2480-group4-22/gson](https://github.com/DD2480-group4-22/gson) \
Gson is a library for Java that can be used to convert Java objects into their JSON representation and JSON strings into their Java object equivalent.
## Onboarding experience
Building the project wasn’t difficult. To build the project either Maven or Gradle has to be installed. The group has used Maven before, it is well documented and easy to use, So therefore we decided to use it. All the dependencies for the project is downloaded and the project is built and tested with "mvn clean package". Some of us had a problem where there would be an error when building the project, but it was resolved by using an older version of java. To build the project Maven is necessary. Building and running the test went smoothly and no unexpected errors occurred. First time it took approximately 2 minutes to build and run the test which seems reasonable, running the test after building took approximately 30 seconds. The project is well documented, but the use of maven isn’t perfectly documented, though using maven is very standardized and well documented so it is easy to know what commands to run to work with the project.

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
One of the main functions of Gson. It reads a JSON object as a stream of tokens. It contains many if-statements and switch-cases which likely leads to the high cyclomatic complexity. This complex function is not super long in terms of code length according to Lizard, only a bit more than a hundred lines. According to the built in word-counter wc JsonReader.java is 1646 lines. This is a big difference from Lizard, but wc counts the lines of the entire document and Lizard only the functions. JsonReader.java contains several functions, which makes wc answer with a much larger number. The code is well documented with JavaDoc and explanations of what each function does. About a hundred lines at the beginning of the JsonReader-document also contains an example of how the code works.

6. **parse** (/gson/src/main/java/com/google/gson/internal/bind/util/ISO8601Utils.java) \
NLOC: 113 \
CCN: 32 \
\
This is a function for parsing and formatting dates in ISO8601 format. Contains many if-statements and switch-cases which likely leads to the high CC. The function is well documented with JavaDoc.

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



### Counted by hand

Every group member also counted the complexity of one of their choosen methods by hand (in total 5 methods):
1. **skipUnquotedValue**: CCN =  #decisions - #exitPoints + 2 = 18 - 3 + 2 = 17.
2. **nextLong**: CCN = E - N + 2 = 15 - 10 + 2 = 7
3. **doPeek**: CCN = 43
4. **peek**: CCN = E - N + 2 = 40 - 23 + 2 = 19

* Add comment regarding if the values match Lizard or not

## Refactoring
Plan for refactoring complex code:
Estimated impact of refactoring (lower CC, but other drawbacks?).
Carried out refactoring (optional, P+):
git diff ...
## Coverage
### Tools
Document your experience in using a "new"/different coverage tool.
How well was the tool documented? Was it possible/easy/difficult to
integrate it with your build environment?
### Your own coverage tool
Show a patch (or link to a branch) that shows the instrumented code to
gather coverage measurements.
The patch is probably too long to be copied here, so please add
the git command that is used to obtain the patch instead:
git diff ...
What kinds of constructs does your tool support, and how accurate is
its output?
### Evaluation
1. How detailed is your coverage measurement?
2. What are the limitations of your own tool?
3. Are the results of your tool consistent with existing coverage tools?
## Coverage improvement
Show the comments that describe the requirements for the coverage.
Report of old coverage: [link]
Report of new coverage: [link]
Test cases added:
git diff ...
Number of test cases added: two per team member (P) or at least four (P+).
## Self-assessment: Way of working
According to the Essence standard of way-of-working our team is in the "working well" phase. We have established good communication and praxis of how to do the work that flows naturally. When assigned to task each team member is available to help one another if necessary and work flow is even. We have developed a understanding between each other and in the beginning we were all strangers but with regular communication we now know how we work and our strengths. Continue to work as we currently do with open communication and helping each other is the plan to move forward. 

## Overall experience
During the course of this project we learnt a lot. We got the chance to work on a larger code base and experience the challenges of it. We also got a better idea on how it can be to contribute to an open source project. This is probably the main take-away from the project and now we have the knowledge to be able to contribute to more open source projects in the future. Apart from that we also learnt about cyclomatic complexity, branch coverage and refactoring.
## P+
What did we do for P+
