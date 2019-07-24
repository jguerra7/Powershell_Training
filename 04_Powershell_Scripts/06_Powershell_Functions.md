
# FUNDAMENTALS OF POWERSHELL FUNCTIONS
In this section we’ll cover the basic concepts and features of PowerShell functions. Functions are the most lightweight form of PowerShell command. They exist in memory only for the duration of a session. When you exit the shell session, the functions are gone. They’re also simple enough that you can create useful functions in a single line of code.

## Functions and scriptblocks
A function, at its simplest, is defined as follows:
```
function <name> {<statement list>}
```  
A scriptblock, at its simplest, is defined like this:
```
{<statement list>}
```
In both cases the braces contain a list of PowerShell statements that are executed when the function or scriptblock is invoked. You’ve seen scriptblocks used with Where-Object and Foreach-Object or the looping and conditional statements in previous chapters. Scriptblocks are covered in more detail in chapter 10.

Looking at the two, you can describe a function as a named scriptblock or a scriptblock as an anonymous function—we prefer the latter.

We’ll start by working through a number of examples showing you how to create simple functions. Take a look at our first example:
```
PS> function hello { 'Hello world' }
```
In this example, hello is a function because it’s preceded by the function keyword. This function should emit the string “Hello world”. Execute it to verify this:
```
PS> hello
Hello world
```
Yes, it works exactly as expected. You’ve created your first command.

Okay, that was easy. Now you know how to write a simple PowerShell function. The syntax is shown in the figure below.

 The simplest form of a function definition in PowerShell
 
![image](https://user-images.githubusercontent.com/47218880/61804144-068ee200-adf9-11e9-88ef-ee85ec2aee24.png)

A function that writes only “Hello world” isn’t too useful. Let’s see how to personalize this function by allowing an argument to be passed in.
