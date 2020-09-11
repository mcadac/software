# Clean Code

- In general, I believe that comments are unnecessary, we developers use comments as an excuse for not properly making our code understandable.
- The next three poins are deeply realted with "Single responsability principel"
- Functions should do one thing. They should do it well. They should do it only.
- Uncle Bob -> "One reason to change" -> If the code inside that function can change for different reasons, then it is doing more than one thing.
- The reason we write functions is to decompose a larger concept into a set of smaller steps.

## Important stuff 

-   We are artist when writting code.
-   A code without unit test is not clean.
-   We have to write code easily to read.
-   We have to tip code thinking in that other person will read this one.
-   Making the code easy to read actually makes it easier to write.
-   It is not the language that makes programs appear simple. It's the programmer that makes the language appear simple.
-   Error handling complete according to an articulated strategy.
-   One difference between a smart programmer and a professional programmer is that
    the professional understands that clarity is king. Professionals use their powers for good
    and write code that others can understand.
-   Every team should have a standard code.

## Meaningful names

-   The names should reveal intent.
-   The name of a variable, function or class, should answer the next questions:
    -   Why it exist.
    -   What it does.
    -   How it is used.
-   Use pronounceable names. (easier when you wanna discuss about the code).
-   Use searchable names.
-   Interfaces and implementations
    -   Avoid use the preceding letter I in the name of an interface.
-   Classes and objects should have noun or noun phrase names like Customer, Account.
-   Avoid words like Manager, Processor, Data, or Info in the name of a Class.
-   A class name should not be a verb.
-   Methods should have verb or verb pharse names like postPayment, deletePage, or save.
-   Accessors, mutators, and predicates should be named for their value and prefixed get, set, and is.
-   When constructors are overloaded, use static factory methods with names that describe the arguments.
    -   Complex fulcrumPoint = Complex.FromRealNumber(23);
    -   Consider enforcing their use by making the corresponding constructors private.
-   Add Meaningful context
    - Good example
       
        Variables with unclear context:

        ````
            private void printGuessStatistics(char candidate, int count) {
                String number;
                String verb;
                String pluralModifier;
                if (count == 0) {
                    number = "no";
                    verb = "are";
                    pluralModifier = "s";
                } else if (count == 1) {
                    number = "1";
                    verb = "is";
                    pluralModifier = "";
                } else {
                    number = Integer.toString(count);
                    verb = "are";
                    pluralModifier = "s";
                }

                String guessMessage = String.format(
                    "There %s %s %s%s", verb, number, candidate, pluralModifier
                );
                
                print(guessMessage);
            }

        ```  

        Variables have a context:

        ````
            public class GuessStatisticsMessage {
                private String number;
                private String verb;
                private String pluralModifier;

                public String make(char candidate, int count) {
                    createPluralDependentMessageParts(count);
                    return String.format(
                    "There %s %s %s%s",
                    verb, number, candidate, pluralModifier );
                }

                private void createPluralDependentMessageParts(int count) {
                    if (count == 0) {
                        thereAreNoLetters();
                    } else if (count == 1) {
                        thereIsOneLetter();
                    } else {
                        thereAreManyLetters(count);
                    }
                }

                private void thereAreManyLetters(int count) {
                    number = Integer.toString(count);
                    verb = "are";
                    pluralModifier = "s";
                }

                private void thereIsOneLetter() {
                    number = "1";
                    verb = "is";
                    pluralModifier = "";
                }

                private void thereAreNoLetters() {
                    number = "no";
                    verb = "are";
                    pluralModifier = "s";
                }
            }
        ```

-   Don't add gratuitous context
    -   The names accountAddress and customerAddress are fine names for instances of the class Address
    but could be poor name for classess.
-   Variables with long scope should have long names.
-   Variables with short little scopes can be abbreviated down even just to one letter.
-   Functions with highly visible scopes, should have short, convenient names. (public functions)
-   Private functions should have long explanatory name.

## Functions

Functions:

-   Small functions between 4 to 6 lines is okay.
-   Functions well named inside classes well named and these clasess live in namesapces well named.
-   readiability first.
-   keep your room clean (our team).
-   Functions should do just one thing.
-   If the function can be split in other small functions, this one is doing more than one thing.
    -   Extract, extract, extract functions from another one.
-   Refactoring book.
-   Function shouldn't have more than three arguments.
-   Don't use boolean as argument of a function... why?... because that means the functions does two things, the firts one when the boolean agument is true, and the second one when the boolean argument is false.

-   Command query separation (Split responsabilities in th rigth way).
-   Step down rule: First public methods and private methods after them.
-   Management dependency. Avoid use swicht statement with polymorphism (OO).  
![management-dependency](/images/management-dependency.jpg)

-   If we need to put a comment to explain what the code does, probably, we should verify and validate the structure of the code, variable names, function names, and do a refactor one more time.
-   The comments can be good on public methods, interfaces, or APIs in order to explain a little bit more what is the prupose of this one.
-   Remove code or comments useless, if we need to go back, Git will help to do it.

## Independent deployment and boundaries

-   Identify when the polymorphism is really good for the system.
-   Identify when and why you really need a swicht statement, this one should exist in a point where doesn't affect the idependent deployment.
-   Protection from new methods and types?
-   (Application --> DB interface layer --> DB):
    -   The application SHOULD NOT depends on the DB interface layer.
    -   The DB interface layer SHOULD depends on the application leve.
-   The database tables are a data structure, they are so concrete and they can't be polyform. (They are data structre).
-   The database doesn't contain domain objects.
-   Unit test reduces the fear to clean the code.
-   Unit test keeps defects under control.
-   TDD is a discipline -> It can improve the production code becuase it allowed that one be testable and descouple.
    -   Write no production code except to pass a failing test.
    -   Write only enough of a test to  demonstrate a failure.
    -   Write only enough production code to pass the test.
-   Production code should be testable.
-   The tests are important as the production code.
    
##  Architecture

-   Architecture: we can see the intend of the system.
-   Use case: way how a user interact with the system to achieve an specific goal.
-   If we wanna an delivery indepent architecture, we should start with delivery indepent uses cases. 
-   Make use cases as asnostic as possible about delivery mechanisms, frameworks, data bases.

##  References
-   https://dev.to/patferraggi/5-clean-code-techniques-you-can-start-doing-today-2ifh
-   https://www.youtube.com/watch?v=NeXQEJNWO5w
-   https://blog.bitsrc.io/solid-principles-every-developer-should-know-b3bfa96bb688
