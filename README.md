# Report for assignment 3
## Project
Name: Gson \
URL: [https://github.com/DD2480-group4-22/gson](https://github.com/DD2480-group4-22/gson) \
Gson is a library for Java that can be used to convert Java objects into their JSON representation and JSON strings into their Java object equivalent.
## Onboarding experience
Building the project wasn’t difficult. To build the project either Maven or Gradle has to be installed. The group has used Maven before, it is well documented and easy to use, So therefore we decided to use it. All the dependencies for the project is downloaded and the project is built and tested with "mvn clean package". Some of us had a problem where there would be an error when building the project, but it was resolved by using an older version of java. To build the project Maven is necessary. Building and running the test went smoothly and no unexpected errors occurred. First time it took approximately 2 minutes to build and run the test which seems reasonable, running the test after building took approximately 30 seconds. The project is well documented, but the use of maven isn’t perfectly documented, though using maven is very standardized and well documented so it is easy to know what commands to run to work with the project.

Since everything went good for all of us running the project we continued on it.

## Complexity
1. What are your results for ten complex functions?
   * Did all methods (tools vs. manual count) get the same result?
   * Are the results clear?
2. Are the functions just complex, or also long?
3. What is the purpose of the functions?
4. Are exceptions taken into account in the given measurements?
5. Is the documentation clear w.r.t. all the possible outcomes?

With the use of Lizard, every group member identified two methods with high complexity (in total 10 methods):
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

Then every group member counted the complexity of one of those methods by hand (in total 5 methods):
1. **skipUnquotedValue**: CCN =  #decisions - #exitPoints + 2 = 18 - 3 + 2 = 17. 


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
Current state according to the Essence standard: ...
Was the self-assessment unanimous? Any doubts about certain items?
How have you improved so far?
Where is potential for improvement?

According to the Essence standard of way-of-working our team is in the "working well" phase. We have established good communication and praxis of how to do the work that flows naturally. When assigned to task each team member is available to help one another if necessary and work flow is even. We have developed a understanding between each other and in the beginning we were all strangers but with regular communication we now know how we work and our strengths. Continue to work as we currently do with open communication and helping each other is the plan to move forward. 


## Overall experience
During the course of this project we learnt a lot. We got the chance to work on a larger code base and experience the challenges of it. We also got a better idea on how it can be to contribute to an open source project. This is probably the main take-away from the project and now we have the knowledge to be able to contribute to more open source projects in the future. Apart from that we also learnt about cyclomatic complexity, branch coverage and refactoring.
## P+
What did we do for P+
