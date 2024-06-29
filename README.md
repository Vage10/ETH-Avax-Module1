# ETH-Avax-Module1
Creating a smart contract that implements the require(), assert() and revert() statements.

Description
There are three methods that constitute the error-handling process in Solidity:

require(): Used to validate certain conditions before further execution of a function. It takes two parameters as an input. However, if the condition fails, then the function execution is terminated and the message (the second parameter) is displayed in the logs. The second parameter, however, is optional. require() will work even if you pass only parameter, that is, the condition to be checked. The require() statement is defined as follows: require( , );

assert(): The assert function, like require, is a convenience function that checks for conditions. If a condition fails, then the function execution is terminated with an error message. assert(<condition to be checked/validated>);

revert(): Can be used to flag an error and revert the current call. You can also provide a message containing details about the error, and the message will be passed back to the caller. However, the message, like in require(), is an optional parameter. revert() causes the EVM to revert all the changes made to the state, and things return to the initial state or the state before the function call was made. The reason for reverting is that there is no safe way to continue execution because something unexpected happened. This is important as it helps in saving gas.

Executing program
First Write the code once you have completed the code Compile it and check if there is any error or not if present resolve the error or you can take help from my code too . After Compilation Deploy it and pass the values in function Check Each Funtion's output .
