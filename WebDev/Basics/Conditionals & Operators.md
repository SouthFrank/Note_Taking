Conditional statements are used for make decisions based on different conditions. By default , statements in JavaScript script executed sequentially from top to bottom. If the processing logic require so, the sequential flow of execution can be altered in two ways:

- Conditional execution: a block of one or more statements will be executed if a certain expression is true
- Repetitive execution: a block of one or more statements will be repetitively executed as long as a certain expression is true. In this section, we will cover _if_, _else_ , _else if_ statements. The comparison and logical operators we learned in the previous sections will be useful in here.

Conditions can be implementing using the following ways:

- if
- if else
- if else if else
- switch
- ternary operator

**If condition**
In JS, the keyword **if** is used to check if a condition is true and to execute the block code. To create an if condition, we need the if keyword, condition inside a parenthesis and block of code inside of a curly bracket `if(condition){code}
![[Pasted image 20231205105906.png]]
**If Else**
If condition is true the first block will be executed, if not the else condition will be executed.
![[Pasted image 20231205111548.png]]
![[Pasted image 20231205111615.png]]
**Else**
Else adds a final condition that executes if none of the others are true.

**Switch Statements**
Switch is an alternative for `if, else if, else`. The switch statement starts with a switch keyword followed by a parenthesis and code block. Inside the code block we will have different cases. Case block runs if the value in the switch statement parenthesis matches with the case value. The break statement is to terminate execution so the code execution does not go down after the condition is satisfied. The default block runs if all the cases don't satisfy the condition.
![[Pasted image 20231205112813.png]]
![[Pasted image 20231205114531.png]]
**Ternary Operators**
Another way to write conditionals is using ternary operators.
![[Pasted image 20231205114906.png]]

#### for loop
The `for loop` is one of the most commonly used statements to repeatedly execute some logic. In JavaScript, it consists of the `for` keyword, a header wrapped in round brackets and a code block that contains the body of the loop wrapped in curly brackets.