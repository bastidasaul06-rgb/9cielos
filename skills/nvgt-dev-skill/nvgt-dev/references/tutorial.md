# Effective Programming and Game Development with NVGT
Please note that this tutorial should be considered a work-in-progress. If you find any issues, alert NVGT collaborators.
File author: Rory Michie

## What is Game Development?
If you are an experienced programmer looking to get skilled up with NVGT as fast as possible, you can safely skip this section.

To someone who has never programmed before, the development of games might seem like an insurmountable task. This manual hopes to help with the steep learning curve of programming, and to get you ready to make the games of your dreams all on your own.

There are many things that need to be considered carefully in the development of a game. One of the most curious is programming; very quickly, programming stops aligning with real-world concepts. The precise instructions and rigid syntactic rules are often the bane of a new programmer's existence.

As you learn, you will begin to "speak" programming more intuitively. You will eventually realize that programming languages are nothing more than a readable abstraction over common paradigms: variables, functions, conditions, loops, data structures, and many more. Start thinking of programming as a new way to think and construct new ideas, rather than a way of expressing already-imagined thoughts and ideas.

And if you don't understand these paradigms yet, don't worry - reading this manual, my hope is that you will learn to make games with nvgt, but I have a secondary goal: by the end of this text, I hope that you will also be confident with programming in general, as well!

Especially in the world of audiogames, whose developers are often small teams at most, skill in game design is correlated with skill in programming; this manual will attempt to teach you both. However, game designing itself can also be made into a career.

When making games, you must first consider what your game will be: what are the rules of the game? Work out your plot and lore, if it has a story. Plan out your project in detail, so that it's easier to turn it into code later on. This is especially true of games that have an underlying narrative.

As well as coding and designing the game, sounds must also be found or created; both free ad commercial sound libraries are available for sound designers of all skill levels.

It is also true that a released game is not necessarily a finished one: multiplayer titles need administration to keep them running, and games might need to be maintained or updated to fix bugs that you did not encounter until post-launch.

## Your First NVGT Script
A script can also be considered one "unit" of code. You have probably seen many of these before: .py, .js, .vbs, perhaps .bgt, and now .nvgt. A script can be executed, meaning that the code contained within will be run by nvgt.

Usually, a game will consist of not just one, but many scripts, each serving some specific function or purpose. For now though, a single script will be sufficient for our needs.

A common tradition among programmers is to write a program that outputs "hello, world!" to the screen, to make sure whichever language they're using is working properly.

Let's do that now and say hello to NVGT!
Open a file in your text editor of choice (I recommend notepad++) and paste the following code inside:
```
void main(){
    alert("hello", "Hello, world!");
}
```
Now, save this file as hello.nvgt, and head over to it in your file explorer.

Press enter on it, and you should see a dialog box appear, with our message inside!

Congratulations. You've just written your first nvgt script!

This script might look simple, but there's actually quite a bit going on here. Let's analyze our various lines:

void main(){ - this is the beginning of a function (more on those later) which doesn't return anything, and takes no arguments, or parameters.

The { afterwards opens a code block. It's customary in many codebases to put the { on the line which opens the block, and to put the closing brace on a new blank line after the block ends.

Inside our block, we have one line: alert("hello", "Hello, world!");

Breaking this line down:
alert() is a function in nvgt that opens a dialog box containing a message. It supports many arguments, but most are optional. Here, we have used the two that are mandatory: title, and text.

We've separated our parameters by a comma and a space, similar to what we do when listing items in English, although we don't need to use "and" like we do in English, and there is only one rule to remember: a comma after every item, except the last.

Our parameters are enclosed in parentheses () but why? This tells NVGT what we'd like to do with the alert function: we would like to call it (calling meaning running the code inside based on some values). Finally, we end the line with a semicolon ; that tells NVGT this piece of code is finished.

Together, alert("hello", "Hello, world!"); is known as one statement, the smallest unit of code that can be executed.
As you can see, functions aren't so daunting after all!

However, there's one missing piece of this puzzle: what's the deal with the main() function?

Actually, it's arbitrary, although extremely common. Many programming languages (rust, c, c++, java, and NVGT, to name a few) require you to use the main() function as what's called the "entry point": in other words, NVGT will automatically call the main function, as we called the alert function. If it doesn't find the main function, it won't know where to start, and will simply give you an error stating as much.

It's very possible to write scripts without a main function. These are sometimes called modules, and sometimes called include scripts, helper scripts, or any number of other names. In NVGT, since a module is quite a different (and advanced) concept, we call them include scripts.

There's something interesting which nvgt can do with this script: not only can you run it, but you can also pack it into an exe file, ready to be shared with whomever you wish to have it. The advantage is that the exe will obfuscate your code and protect it from bad actors, which is especially useful for multiplayer projects!

Not just that, but anyone can run your game if you compile it, whether or not they have nvgt installed on their computers.

It's easy to do: when you've selected your script in windows explorer, don't run it. Instead, press the applications key (alternatively shift+f10 if you don't have one of those) and a "compile script (release)" option should appear.

Click it, and a new file should appear next to the script: hello.zip.

As you may know, a zip file is a compressed archive containing multiple files. When one compiles scripts with NVGT, the resulting archive file will include libraries on which NVGT depends, project assets, and of course the main executable.
The heart of nvgt includes its bundling facilities, its sound engine, its input handlers and other such things. The mind of the engine is the scripting language, AngelScript, which must be explored before we can truly understand how NVGT works.
So, we will devote a chapter to some fundamental concepts.

## Fundamentals of AngelScript

I will now explain the nvgt and programming concepts we'll need to understand the rest of this tutorial, using some short examples. They are called snippets, and won't all run. They are just to demonstrate.
This section will be long and perhaps boring for some. However, after you have read it, you will be able to move on to more immediately fruitful learning.
Don't be ashamed if you need to read over a section twice or even several times to understand it. The important thing is to have a rich and meaningful comprehension of AngelScript, so that you don't struggle later. It may help you to know that some experienced programmers may choose to read manuals multiple times, to make sure they get everything that might be involved in a project.

### comments
Sometimes, you might want to document what a particularly complex bit of code does, or perhaps remind yourself to make it better later.

For these reasons and more, programming languages usually have some way of keeping notes in your code that they will not attempt to execute.

These are usually called comments, and nvgt has three types of them:

The single-line comment is written with a //, and looks like this:
```
// Hello!
```
The multi-line comment is written slightly differently, enclosed by a /* and a */. It looks like this.
```
/*Hello!
This is a multiline comment.
You can make this as many lines as you want.
Just don't put a star and slash next to each other in that order, or it may not end where you expect.
It lasts for a while.*/
```
Lastly, the end-of-line comment is sort of like a single-line comment, but goes after a line of code. For example:
```
int drink_price=5; // Should this be able to store fractional values?
```

As well as documenting your code, comments (especially multi-line ones) can be used to surround code which doesn't need to be run, or is broken for some reason.

This is called "commenting out" code. Code which is commented out will be ignored by the compiler, just like regular textual comments.

Example:
```
void main(){
//alert("hello", "hello, world!")
alert("how are you", "My name is NVGT!");
}
```
If you run this, you will only get the "how are you" dialog box, and not our "hello" one. You see, I made a little error when I was writing that line; can you spot why I might have commented it out?

### include scripts
The truth about programming, as with anything, is that organization is a big part of success. Always remember this: reading code is more difficult than writing it.

As a programmer, your highest-priority task is to get the code working; arguably just as important is to keep it working.

Imagine you are a version of yourself, with similar programming experience. However, you have never read your project's code before. If you can intuitively understand what all of its components do, then you have succeeded in writing readable code!

Another thing experienced programmers like to have is modularity. This philosophy dictates that as little of your code as possible should depend on other code.

Include scripts are how we achieve modularity in nvgt: by using the #include directive at the top of your program, you can load in another file of code, adding its code to your own in doing so.

NVGT ships with a host of include scripts (or includes for short), which you are free to use to speed up the process of game development.

For example, the speech.nvgt include has functions for making your game speak out text, without needing to worry about what screen reader or sapi voice the user has.

Some of these scripts are modified versions of those included with BGT; this tutorial won't talk about them very much, but many are documented.

If you wanted to use the speech.nvgt include, you would put it at the very top of your script, like this:
```
#include "speech.nvgt"
```

Why the #? In nvgt, # signifies what's called a preprocessor directive: usually one line of code, these are used before your program is run to change something about it.

NVGT has what's called an include path. It searches multiple folders for your include scripts, and if it can't find them, it will give you an error. It works a bit like this:
1. Search the directory of the script from which another script was included
2. Search the include folder in nvgt, in which all the built-in includes are stored.
[add more later here maybe]

Here is a full code example you can copy into an nvgt script and run.
```
#include "speech.nvgt"
void main(){
    speak("Hello with the NVGT speech include!");
}
```

### variables
If you know about variables in algebra, then you will have a similar concept in your head to those in programming. They are, at their core, names for data. There is one difference: in algebra, we don't always know what a variable represents exactly. In NVGT, they can only ever have one specific value.

Quite a few things in nvgt are variables: functions, normal variables, classes and many more.

In this section we will learn about how to make some simple variables, and how to change them.
#### integers (ints) and unsigned integers (uints)
In NVGT, there are two main types of numbers, integers and floating-point numbers.

The easiest to understand is an integer, otherwise known as a discrete number. We'll learn about those first, then move on to floats.
Here are some examples of declaring the two kinds of integers:
```
int x = 3;
x = -3;
uint y = 3;
y=-3; // Oh no!
```
As you can see, we used both kinds of integers. One is called an int, as we'd expect, but the other is called a uint. What does the u mean? You might have already guessed: unsigned!

Unsigned means that a sign bit is not used. That leaves one more bit for the value and hence doubles the possible range in the positive direction. However, you may not store negative numbers in unsigned integers.

Now, let's break down our int declaration statement

`int` is the type of variable (int)

`x` and `y` are the "identifier" of a variable. In other words, its name.

`=` is the assignment operator. The first time you assign a value to a variable, it is called initialization.

After the =, a value is assigned to the variable. Then, the ; is used to end our statement, making it complete and ending the line.

You'll notice that only the first reference of a variable needs its type: it's the declaration of the variable, whereas the second line is a reassignment of the same variable.
If you include the type at the beginning, you would create a new variable which would "shadow" the old one. This is syntactically valid, but could cause unexpected behavior.

You may also declare what are called global variables. I'll give a full example to demonstrate this.
```
int unread_emails = 20;
void main(){
    alert("important", "You have " +unread_emails + " unread emails.");
}
```
As you can see, despite the fact that the global variable was not declared within the function (or its scope), we can still use it. If declared outside a function, a variable's scope is global (as opposed to local): it can be accessed from all functions in your program.

This author personally does not recommend much usage of globals. A more elegant way to use variables in lots of different functions at once will be demonstrated shortly. The exception is consts, which will also be discussed later.

To create the message, I used the string concatenation operator to glue one string, one variable, and another string together. This will be further explained in the section on Strings.

As we know, inside a function (but not outside) variables can be changed, or re-assigned. You might have realized that changing a variable's value in relation to itself (like giving the player some money or points) is a handy side effect, since you can simply reference a variable when re-assigning it, like this:
```
int level = 2;
level = level + 1;
```
But there is a simpler, more readable way of doing this, which saves lots of time (and cuts down on typos!). 

If you want to change a variable in relation to itself, you use what's called compound assignment.

This combines an operator, like an arithmetic operation or string concatenation, with the assignment operator.

For example, we could rewrite our previous code using compound assignment:
```
int level = 2;
level +=1;
```
As you can see, it's much cleaner!

Here's a full example to consolidate what we've learned. You can copy and paste it into an nvgt script and run it. We'll also demonstrate includes and comments again.
```
#include "speech.nvgt"
int g = 3; // a global variable
void main(){
    /*
    This program demonstrates integers in NVGT, by declaring one (a) and performing a variety of arithmetic operations.
    After each operation, the value of a will be spoken.
    */
    int a = 0; // This is the variable we'll use. 
    speak("a is now " + a);
    a+=2;
    speak("After adding 2, a is now " + a);
    a*=6;
    speak("After multiplying by 6, a is now " + a);
    a /=3;
    speak("After dividing by 3, a is now " + a);
    //something new!
    a -= g;
    speak("After subtracting g, a is now " + a);
}
```

##### Bonus: Integer Range Table
You may refer back to this table whenever you want to choose which type of integer you're going to use. Remember that you don't have to use a single type throughout your entire project; select the best fit for the job on a per-variable basis.

Table of ints and their ranges:
| Type    | Size (bits) | Minimum Value | Maximum Value |
|---------|-------------|---------------|---------------|
| int8    | 8          | -128          | 127           |
| uint8   | 8          | 0             | 255           |
| int16   | 16         | -32,768       | 32,767        |
| uint16  | 16         | 0             | 65,535        |
| int32   | 32         | -2,147,483,648| 2,147,483,647 |
| uint32  | 32         | 0             | 4,294,967,295 |
| int64   | 64         | -9,223,372,036,854,775,808 | 9,223,372,036,854,775,807 |
| uint64  | 64         | 0             | 18,446,744,073,709,551,615 |

#### float variables

The main difference between ints and floats is that floats can store fractional values, whereas ints are restricted to exclusively whole numbers. Although they do come with some drawbacks, this makes floats more suitable for tasks where a high level of precision is needed. They are also useful for dealing with imprecise, but extremely large, numbers.

There are two main types of floats in nvgt: float and double.

Float is a 32-bit (or single-precision) variable, and double is a 64-bit variant which can store a greater number of decimal digits and higher exponents.

In most cases, you should be okay to use a double, but this is not always required and is often not a good choice anyway.

The inner workings of floats are well beyond the scope of this tutorial, but it's enough to know that computers don't think about fractional values like we do: the concept of decimal does not exist to them.

Instead, they use a binary representation, called the IEEE754 standard.

You cannot rely on floats storing a number perfectly. Sometimes, the IEEE754 standard has no exact representation for a number, and its closest equivalent must be used instead.

To demonstrate this, run this script. The result should be 1.21, but it isn't.
```
#include "speech.nvgt"
void main(){
    double result = 1.1 * 1.1;
    screen_reader_speak(result, false); // implicit cast from double to string
}
```
As you can see, the value is very close, but not quite right. We even used the double type, with 64 bits of precision, but it wasn't enough.

To understand this limitation of binary, consider that decimal also has similar limitations. The value of 1/3 can never be notated exactly in decimal form: you would need an infinite number of 3s - 0.33333....

There are several ways to alleviate this problem, but for the moment we don't have to worry about them.

#### string variables
The easiest and most reliable way to think about string variables is that they are text. "hello" is a string, "this is a test" is a string, and "1" is a string (this last one is confusing but will be explained shortly).

We have actually seen string variables before. When we were making our hello world program, we used two of them for the title and text parameter to the alert function.

Now knowing about variables and their identifiers, you can probably see why we used quotes (") around them, and why that is necessary.

If we hadn't, "hello, world!" would've ended up being interpreted as two function parameters, the variable identifiers hello and world, neither of which existed in the program.

NVGT would not have liked this at all; in fact, it would've thrown numerous errors our way in response.

So, quotes must enclose strings to let NVGT know that it should ignore the text inside - the computer doesn't need to know that it's text, only that it's data like text, which it can then show to the user for them to interpret.

It's almost, if not quite, like delivering letters: you don't care about or have the information in a letter (and if you did, then your manager probably needs to talk to you!) but the letter's recipient will. It could be in English or Chinese or Braille or scratch-and-sniff stickers but you will never know.

Similarly, NVGT will happily place text in quotes in strings, which can then be passed to functions, put into variables, or concatenated onto other variables or strings.

In this case, it was assigning them to the title and text variables, arguments of the alert function.

String variables are created using a similar syntax to the int variable we just saw:
```
string name = "Alice";
```
You can also create a string with multiple words:
```
string message = "How are you today?";
```
Or even a string with Unicode characters:
```
string message2 = "Hello, and 你好 👋";
```
Just like integer variables, strings also have operations which can be performed on them. By far, the most common is concatenation.

Concatenation is the process of stringing strings together. The + symbol is used for this, and compound assignment with += is also supported.

Let's see how it works:
```
string sentence = "The quick brown fox";
sentence += " jumps over the lazy dog.";
```
To give you some familiarity with string concatenation, let's go over a full example. Copy this into an NVGT script, and run it:
```
#include "speech.nvgt"
void main(){
    int a = 1;
    int b = 2;
    string c = "1";
    int d = 2;
    string result1 = a + b;
    string result2 = c + d;
    speak("a + b is " + result1);
    speak("c + d is " + result2);
}
```
The output should be:

a + b is 3

c + d is 12

Is that what you expected?

What's happening here is called conversion, specifically implicit or automatic casting/conversion. In programming, casting means converting some value of one type (int) to another type (string).

When we calculate result1, we perform addition on a + b (1 + 2) and get 3, which makes sense.

But when we calculate result2, NVGT automatically converts d, an int, into a string, making it "2", so it can be concatenated.

It then ignores the data inside, and just adds it together. So, instead of having 1 + 2, you get "1" + "2" - which is just two pieces of data combined together into one string, making "12".

This is why strings are so useful: they can hold any data in a text-like form, and then the meaning of that data can be interpreted by something else. In this case, it is output to our screen readers, and we interpret it.

#### boolean variables (bool)
Leading up to a powerful idea called conditionals, boolean variables are another fundamental datatype in programming, and are usually present in some form in programming languages.

Named in honour of the mathematician and logician George Boole, the variables can store only two possible values: true or false; 1 or 0, on or off, yes or no.

They are extremely powerful and there are quite a few things you can do with them, but most don't really make sense without conditionals. Still, we can try a basic example, using not (!), a logical operator:
```
void main(){
    bool state = true;
    speak("State is: " + state);
    state = !state;
    speak("Flipped, state is: " + state);
}
```
This shows how to declare a bool: it's fairly similar to other variables. Unlike strings, the values true or false do not need to be put in quotes, despite the fact that they are not variables in the traditional sense. True and false are actually consts, which means you can never accidentally overwrite their values; trying will yield an error.

Those are enough types for now. We will learn about more later on.
#### Const And Enum Keywords
In this section, the last things we will explore regarding variables are consts and enums.

Const variables (or constants) are a special kind of variable, whose value cannot be changed beyond the first assignment. In other programming languages they may be called immutable.

They are particularly useful in avoiding "magic numbers": using numbers directly in our code is bad!

Let's write some code to demonstrate:
```
#include "speech.nvgt"
void main(){
    speak("Welcome to the camping store! You need to have 30 dollars to buy a folding chair.");
}
```

This looks fine, but we're using this value in only one area of our code (mostly because there is only one place in which to use it, but that's beside the point).

Suppose, now, that we use the value 30 in many areas: not just telling the user how much it is to buy a chair, but also for the logic of buying and selling them itself.

It's also valid in that it works, but it is frowned upon.

Consider: inflation is making everything more expensive these days, so what if we need to raise this price to 35 dollars next year?

The answer to that question is that it would be a coding nightmare! We would have to go through our code, painstakingly changing every reference of the value 30 to 35. But we could get it wrong: we might accidentally make one of the values 53, or change the number of centimeters in a foot from 30 to 35 in our frantic search - wouldn't it be much better if we only had to change the value once?

This is where consts will save the day!

Using them , we could rewrite our code like this:
```
#include "speech.nvgt"
const int price_folding_chair = 30;
void main(){
    speak("Welcome to the camping store! You need to have " + price_folding_chair + " dollars to buy a folding chair.");
}
```
Much better; now we can use this value wherever we want to, and all we have to do to change it is update the one declaration at the top of the file!

To declare a variable as const, simply precede the type with the word "const" followed by a space, just like in our example.

Another similar concept is that of \*enumerations\*: in NVGT, they are special types with a set of specific values.

Each of their values can be resolved to but never changed.

They actually map to integers, with the first value being 0 and the second being 1. Where required, this can be changed. However, there is a downside to this property.

There is no guarantee that a variable of an enum type will actually hold one of its specific values: it might hold any other arbitrary integer value.

Nevertheless, they can be great for organization. Besides, even if the value is arbitrary, there's no chance of some random integer being implicitly converted to an enum; only explicit conversion is supported.

Note: while integers can only be explicitly converted to enums, enums can be implicitly and explicitly converted back to integers. This helps with backwards compatibility.

AN example of an enum:
```
enum directions{
    direction_east,
    direction_north=90,
    direction_west=direction_north*2, // Just because I do doesn't mean you should, but you can
    direction_south=270}
```
It is common practice to pretend all enum value names with something similar to the name of the enum itself. A prefix doesn't have to be exactly the same, but it should be close to it.

For instance, one NVGT enumeration is `key_code`; all its possible values are prefixed with `key_`.

This is done for clarity, convention's sake, and backwards compatibility reasons.
##Conditionals And The If Statement
The if statement is perhaps one of the most overwhelmingly useful pieces of code. Its ubiquity is almost unparalleled and a variation of it can be found in just about every programming language in use today.

Say you want to run some code, but only in certain cases; the if statement is what you use. Let's give a full example:
```
#include "speech.nvgt"
void main(){
    int dice = random(1, 6);
    if(dice == 1)
        speak("Wow, you got " + dice + "! That's super lucky!");
    else if(dice < 4 )
        speak("You got " + dice + " - that's still pretty lucky, but aim for a 1 next time!");
    else
        speak("Ah, better luck next time. You got a " + dice + ".");
}
```
This small dice game is very simple. Roll a dice, and see how low a number you can get.

There are three options: you get a 1 (the luckiest roll), 2 or 3 (the 2nd luckiest), or 4-6 (which means you lose).

We can express these three cases using the "if", optional "else if", and optional "else" constructions. They work like this:

if(conditional)

statement/block

else if(conditional)

statement/block

else if(conditional)

statement/block

else

statement/block

That's right - in each of these structures, there can be one \*if\* case, an unlimited number of \*else if\* cases (or none), and either no or one \*else\* case.

These are slightly different than normal statements, because the if, else if, and else parts don't have semicolons. Only the code "inside" each case needs semicolons at the end.

But what is a conditional?
A conditional is any value that returns either true or false. This can be something which is already a bool variable, or the result of a comparison operator.
There are eight comparison operators in nvgt. Each takes two values and returns true or false based on their relationship.
| Operator | Purpose                                              | Opposite |
|----------|------------------------------------------------------|----------|
| ==       | Checks if two values are exactly equal               | !=       |
| !=       | Checks if two values are not exactly equal           | ==       |
| <=       | Checks if a value is less than or equal to another   | >        |
| >=       | Checks if a value is greater than or equal to another| <        |
| >        | Checks if a value is greater than another            | <=       |
| <        | Checks if a value is less than another               | >=       |
| is       | Checks if two handles point to the same object      | !Is       |
| !is       | Checks if two handles don't point to the same object| is       |

There are also four logical operators that work on bools, one of which we explored in the section on booleans. They are:
* && (and) returns true if the bools on the left and right are both true, but not neither or just one
* || (or) returns true if either or both of the bools on the left or right are true
* ^^ (xor) returns true only if one of the left and right bools is true, but not neither or both
* ! (not) returns the opposite of the bool on the right (it takes only one bool and nothing on the left)

Using these comparison operators and logical operators is how you create conditionals to use in if statements, though remember that bools themselves can already be used directly.

This is all a lot of information at once, so here's a full example to demonstrate:
```
#include "speech.nvgt"
void main(){
    int your_level = 5;
    int monster_level=10;
    int your_xp=50;
    bool alive=true;
    if(alive)
        speak("You are alive!");
    if(monster_level<=your_level){
        speak("You manage to kill the monster!");
    }
    else{
        speak("The monster is higher level than you, so it kills you!");
        alive=false;
    }
    if(!alive)
        speak("You are no longer alive!");
    if(your_level*10==your_xp)
        speak("Your level is equal to a tenth of your experience points.");
}   
```
This example demonstrates an important distinction we touched onon earlier: if statements which use a block instead of a single statement need to have the block surrounded by braces.

Where a block might be used, a single statement can usually be used as well; the exception is functions, which must always use a block, whether or not it is a single line.

### loops
While the if statement is used to create conditional checks for whether certain pieces of code will be run, loops are used to repeat sections of code more than once.

Loops have many uses, including infinite loops (which are already a well-known concept), loops that run a known number of times, and loops that we use to run through certain data structures like arrays.

NVGT has four main types of loop, three of which we will discuss in this section: while loops, do-while loops, and for loops. We will also discuss the break and continue statements.

The foreach loop will be covered later.
#### While Loops
The most simple form of loop is the while loop. It is written almost exactly the same as the if statement, and runs exactly the same - except that it will check the condition and run the code over and over, checking before each run, until the condition is determined to be false.

Here is an example which you can run:
```
#include "speech.nvgt"
void main(){
    int counter = 1;
    while(counter <6){
        speak(counter);
        wait(1000);
        counter+=1;
    }
}
```
This should speak out the numbers 1 through 5, with a second's delay between each.

Just like if statements (as well as other types of loops), a while loop can also be written with only one line of code inside. If so, it does not need to be surrounded by braces.

The while loop is the standard way to write an infinite loop: a piece of code that will run forever, perhaps until broken out of with the break keyword.

To make an infinite loop, we simply use
```
true
```
as the condition, since it will logically always return true, every time.

#### Do-While Loops
In while loops, the condition is checked before the code is run. This means that, just like an if statement, there is always the possibility that the code may never run at all.

On the other hand, in do-while loops, the condition is checked after the code has run. As a result, code will always run at least once.

It's often up to the programmer which type they think is best, and there is no real standard. Whichever is more convenient and maps best to the situation can be used, and neither has a performance advantage over the other.

Let's rewrite our counter example using a do-while loop:
```
#include "speech.nvgt"
void main(){
    int counter = 1;
    do{
        speak(counter);
        wait(1000);
        counter+=1;
    } while(counter < 6);
}
```
As you can see, since the condition is at the end, we need to check it based on the value after the counter as updated, instead of before.

If we had used
```
while(counter < 5);
```
as we had done with our while loop, the code would have only counted to 4, since the counter gets updated after it speaks its current value.

#### For Loops
One of the most-used types of loop is something similar to our counter example from earlier in this chapter.

There are a lot of lines here that for loops can compress into just one line; they make code easier to write as well as read later on.

For loops also have an additional unique property, which is extremely useful, but will be discussed in a moment after some background.

However, they are admittedly difficult to grasp at first, because they're very different than both the while and do-while loops.

Consisting of four parts, a for loop might look like this:
```
for(declarations; condition; final)
statement/block
```

How it works:

1. The declarations code is run, and a variable (or more) is declared.
2. The loop starts to run.
3. At the beginning of each loop iteration, the condition is checked. If false, the loop stops, potentially even before it has run once.
4. Assuming the condition is true, The code inside the for loop is run.
5. After that code has finished, the final step is run.
6. Repeat steps 3-5

Note: all three parts of a for-loop are optional. For instance, you may omit the declaration by simply writing nothing before the first ;

As you can imagine, a for loop would help us rewrite our counter example in a much more readable way.

Let's go ahead and do this now:
```
void main(){
    for(uint i = 1; i < 6; i ++){
        screen_reader_speak(i, false);
        wait(1000);
    }
}
```

This example will yield the same results as the previous one, but it does it in a manner that is more concise. Pretty code is very important for your sanity!

#### Break And Continue Statements
There are times when you might want to get out of loops completely. This is called "breaking out", and it's very easy to do:

```
break;
```
There are no additional components to this statement, as there are in some other languages such as rust.

This is particularly useful in infinite loops (typically created by simply using true as the condition in a while loop)

When this is done, the loop immediately ends, and will iterate no longer.

If you want to break out of a loop, but still want it to try and run again (IE. not run the rest of this iteration), the continue statement can help.

As is the break statement, the continue statement is simply written on a line by itself:
```
continue;
```
This immediately ends the current iteration. In while and do-while loops, nothing more happens, and the final component in a for loop is run. Then, the next iteration may begin.

The reason that for loops behave differently is by design. It is neither easy nor proper to achieve this behavior in any other way.

### functions
Functions in nvgt are pieces of code that can be "called" or executed by other parts of the code. They take parameters (or arguments) as input, and output a value, called the "return value".

The return value is so named because it gives some critical piece of information back to the calling function, without which work cannot continue.

Let's use baking a cake as an example: in the process of baking a cake (simplifying greatly) you put the batter in the oven. The oven cooks the cake, and then you open it up and take a cooked cake out.

You can't do something like cooling the cake while the oven is baking, because you just can't: the oven is baking the cake. In the same vein, only one function can be running at once, and we say that function is currently executing.

When a function ends, execution returns to the function that called it, just like taking the cake back out of the oven. It returns, along with execution, whatever is specified using a return statement (discussed shortly).

Here is a snippet for the purpose of example:
```
int add(int a, int b){
    return a + b;
}
```
Frankly, the example is a needless abstraction over an already-simple task (the addition operator) and you should almost never do it like this in production. Aside from that, it's a good example of a task functions are capable of performing: it takes data in, and then outputs some other data.

The way we declare functions is a little bit strange, and this example is packed with new ideas, so let's break it down piece by piece:

int add(

The beginning of the function's declaration, letting the compiler know that it is a function with the return datatype (int), the name (add) and the left parenthesis

int

the type of the first variable

a, 

the name (identifier) of the first parameter/argument variable, and a comma and space to separate it from the next variable, just as we use when calling functions

int b)

The declaration of the second parameter/argument variable, another integer, and a right parenthesis to tell the compiler there are no more parameter variables

{

The beginning of our function (remember, there must always be braces enclosing functions, even if the execution step is only one line in length.)

Then, the next line:

    return a + b;

This is the only line in our function, and returns an expression evaluating to an int variable. It adds the a and b variables' values together.

}

The end of our function, which lets the compiler know that we're back in the outer scope (probably global)

As your projects grow in complexity, you'll often find yourself wanting to create functions that can handle different types of input, or functions that have optional parameters to make them more flexible. AngelScript provides two powerful mechanisms to achieve this: function overloading and keyword arguments.

#### Function Overloading
Function overloading allows you to create multiple functions with the same name, as long as they have different parameter lists. This is particularly useful when you want a function to behave differently depending on what type of data you pass to it, or when you want to provide multiple ways to call the same logical operation.

The key to overloading is that each version of the function must have a unique "signature" - that is, a unique combination of parameter types and/or number of parameters. The function name alone is not enough to distinguish them.

A simple example to demonstrate:

```
#include "speech.nvgt"

// First version: takes two integers
int add(int a, int b) {
    return a + b;
}

// Second version: takes three integers
int add(int a, int b, int c) {
    return a + b + c;
}

// Third version: takes two doubles
double add(double a, double b) {
    return a + b;
}

// Fourth version: takes two strings (concatenation)
string add(const string&in a, const string&in b) {
    return a + b;
}

void main() {
    speak("Two integers: " + add(5, 3));
    speak("Three integers: " + add(5, 3, 2));
    speak("Two doubles: " + add(5.5, 3.2));
    speak("Two strings: " + add("Hello", " World"));
}
```

When you run this, NVGT automatically chooses which version of the `add` function to use based on the types and number of arguments you provide. This is called "overload resolution."

But what if you want a function that can accept optional parameters? That's where default parameter values come in.

#### Default Parameter Values
You can specify default values for function parameters to make them optional when calling the function. If a parameter has a default value and you don't provide an argument for it, the default will be used instead.

I will demonstrate:
```
#include "speech.nvgt"

void greet_player(const string&in name, const string&in greeting = "Hello", bool enthusiastic = false) {
    string message = greeting + ", " + name;
    if (enthusiastic) message += "!";
    speak(message);
}

void main() {
    greet_player("Alice");                          // Uses defaults: "Hello, Alice"
    greet_player("Bob", "Hi");                      // "Hi, Bob"
    greet_player("Charlie", "Welcome", true);       // "Welcome, Charlie!"
}
```

Default parameters must appear at the end of the parameter list. You cannot have a parameter with a default value followed by one without a default value.

#### Keyword Arguments
One of the most powerful features for making your functions flexible and readable is keyword arguments. These allow you to specify parameters by name when calling a function, rather than relying purely on their position.

This is particularly useful when you have functions with many parameters, or when you want to skip some optional parameters while providing others.

A quick note before we move on to an example: if you find yourself with functions taking too many parameters, consider whether it might be better to use a configuration class to store them all. This has numerous advantages and will be demonstrated in the object-oriented programming tutorial.
```
#include "speech.nvgt"

void configure_player(const string&in name, int health = 100, int mana = 50, bool flying = false, int level = 1) {
    string status = name + " (Level " + level + "): " + health + " health, " + mana + " mana";
    if (flying) status += ", flying";
    speak(status);
}

void main() {
    // Traditional positional arguments
    configure_player("Alice", 80, 40, true, 5);
    
    // Using keyword arguments - much more readable!
    configure_player("Bob", health: 120, level: 3);
    configure_player("Charlie", flying: true, level: 7, mana: 80);
    
    // You can mix positional and keyword arguments, but keywords must come last
    configure_player("Diana", 90, level: 4, flying: true);
}
```

As you can see, keyword arguments make function calls much more self-documenting. When you see `flying: true`, you immediately know what that parameter controls, whereas with positional arguments, you'd need to check the function definition.

#### Combining Overloading with Default Parameters
You can combine function overloading with default parameters to create very flexible APIs. However, be careful not to create ambiguous situations in which NVGT can't determine which overload you intended to call.

```
#include "speech.nvgt"

// Create a player with just a name
void create_player(const string&in name) {
    speak("Created player: " + name);
}

// Create a player with name and level
void create_player(const string&in name, int level) {
    speak("Created level " + level + " player: " + name);
}

// Create a player with all stats
void create_player(const string&in name, int level, int health, int mana = 50) {
    speak("Created level " + level + " player: " + name + " (" + health + " HP, " + mana + " MP)");
}

void main() {
    create_player("Alice");
    create_player("Bob", 5);
    create_player("Charlie", 3, 80);
    create_player("Diana", level: 7, health: 120, mana: 75);
}
```

#### Things To Keep In Mind
When using function overloading and keyword arguments, be aware of the principles outlined in this section.

For overloading:
* Only overload functions when the different versions perform logically similar operations
* Avoid creating overloads that could be ambiguous - NVGT should always be able to determine which version you want
* Consider whether default parameters might be a better solution than overloading

For keyword arguments:
* Use descriptive parameter names that clearly indicate their purpose
* When calling functions with many parameters, even if you set most of them, I advise that you explicitly state which parameter is which by using it as a keyword argument
* Remember that keyword arguments must come after all positional arguments in a function call
* If you feel like it, you can use some or all positional arguments in the "wrong order" by stating their names as keyword arguments. Do this judiciously.
* Every positional argument must still be specified somewhere!

For default parameters:
* Choose sensible defaults that represent the most common use case
* Document what the default values mean, especially if they're not immediately obvious

#### A Practical Demonstration
Let's put this all together with a more realistic, runnable example; here is a function for creating game alerts:

```
#include "speech.nvgt"

void show_alert(const string&in message, const string&in title = "Alert", bool interrupt = true, int duration = 0) {
    // In a real game, this would show a proper alert dialog with keyboard handling and such.
    string full_message = title + ": " + message;
    if (duration > 0) full_message += " (Auto-close in " + duration + "s)";
    
    speak(full_message, interrupt);
    if (duration > 0) wait(duration * 1000);
}

void main() {
    // Simple alert
    show_alert("Game saved successfully!");
    
    // Custom title
    show_alert("Low health warning", title: "Warning");
    
    // Non-interrupting with auto-close
    show_alert("Achievement unlocked", interrupt: false, duration: 3);
    
    // All parameters specified
    show_alert("Critical error occurred", title: "Error", interrupt: true, duration: 5);
}
```

If you can learn to take advantage of these features, you will create code that is easier to use and more flexible. They are cornerstones of advanced NVGT programming and are used extensively in the core engine itself.

#### Bonus: Some notes About References (Advanced)

If you are new, you can skip this brief section, especially because it is discussed in another article in great depth for deeper and easier understanding.

There are a couple of common misconceptions and mistakes made by even experienced coders when it comes to function parameters.

For performance, it may seem intuitive to declare your primitive parameters as const x &in references, but this is almost always useless, except in the case of (say) strings or vectors when the value itself is likely larger than 8 bytes.

The reason for this is the fundamental nature of a reference: a pointer itself is a value of 8 bytes storing a memory address. As opposed to most primitives (ints etc), there is no advantage, as the new bytes still need to be allocated - it is just a different value that is placed into them (the address instead of a copy of the value).

### Arrays (Lists)
If you have programmed prior to reading this manual, you may have seen them before: an array is angelscript's equivalent to a vector or a list.

Via this powerful data structure, we can store lots of the same type of variable in one neat package.

In NVGT, arrays are dynamic. This means that you can add and remove from them at any time you'd like, as opposed to arrays in (say) c or rust, which are trickier to expand or remove from.

Before we move on to a summary of their methods, here is a quick example of iterating through an array with a foreach loop:
```
void main(){
    int[] scores = {20, 30};
    scores.insert_last(50);
    screen_reader_speak("The scores of the players in this game are:", false);
    foreach(int& x:scores)
        screen_reader_speak(x, false);
}
```
There is also an older version, which is more convoluted-looking but lets you see the index of the item you're working with:
```
void main(){
    int[] scores = {20, 30};
    scores.insert_last(50);
    screen_reader_speak("The scores of the players in this game are:", false);
    for(uint i = 0; i < scores.length(); i ++)
        screen_reader_speak(scores[i], false);
}
```
There are two ways to declare arrays:
```
type[] name;
```
or
```
array<type> name;
```
Neither is better than the other, but pick one and stick to it as much as possible throughout a project.

If you want to initialize an array with some number of values already inside, there are two ways to do that:

An array literal-
```
int[] numbers={10, 20, 30, 40, 50, 60};
}
And an array constructor-
```
int[] ten_zeroes(10);
```
That line of code will make an array of ten integers (indexed with 0 through 9). Since this method creates uninitialized values, they will all be set to 0.

If we had done the same thing with an array of ten strings, we would've gotten ten empty strings, and so on.

The variables in an array are called "items" or "elements", and you can imagine them as being stored in a line (ordered).

As a consequence, we can access the 1st, 2nd, or any other item in our line of elements, via "indexing".

Slightly more complicated to think about, however, is that arrays in NVGT use "0-based indexing".

This is true of most programming languages, with a notable exception being lua.

0-based indexing means that, instead of the 1st item being at index 1, it is at index 0. Item 2 would be at index 1, item 3 at 2, and item 20 at 19.

### Object-Oriented Programming (OOP)
We humans are creatures of order. We like putting things into categories that make it easier to express their properties and relationships.

So, despite the daunting title of this chapter, we will now be learning about a way to simplify your code - not complicate it.

Object-oriented programming is a philosophy which posits that many things in code can be expressed as "objects". The way AngelScript implements it, there are two distinct components to objects:
* A class is like a type of object (a blueprint, if you will). It can store information about what that object is (its parent), has (some variables and properties), and does (methods).
* An instance is a "real" object itself.

That explanation may have been somewhat empty of meaning if yu aren't familiar with OOP. Considered another way--

A class only exists in the theoretical sense. For example, you know what an apple is, has, and does:
* It \*is\* a fruit; a fruit \*is\* a food; a food \*is\* something you can pick up and hold in your hand (however messily). Something you can pick up and hold in your hand (however messily) \*is\* something in our universe.
* It \*has\* seeds, and it might \*have\* a sticker on the outside. It \*has\* a red or green color, most likely.
* It \*does\*...well, pretty much nothing we'd immediately observe. It's a fruit, after all; what more do you want from it?

You may have noticed that I could've chosen any level of specificity for what an apple \*is\*, and this is quite useful. You need not create classes for every level of specificity, unless those levels are somehow distinctive in your world.

If you know for a fact that your game will only ever need apples, then there is no reason for it to know apples are fruits or anything else.

Alright - we know what an apple is, has, and does. That means we could have a pretty good go at making a class describing it in code-form.

Does it mean we have an apple? Not necessarily. We could have one, but we might not, even if we know what they are.

In the same way, there being a class does not automatically create any instances of said class in your code.

#### Creating Classes
The simplest definition of a class:
```
class pizza{}
```
This is a completely empty class. It doesn't do anything and is useless.

I'll make things more interesting: we can put variables in our class.

class pizza{
    string taste;
    bool is_good=true;
}
Okay, that's fine. But we always need a way to create them. We'll add a \*constructor\*: a special nameless function that creates members of our class - and then, let's actually use it.

You can run this example:
```
#include "speech.nvgt"
class pizza{
    string taste;
    bool is_good=true;
    pizza(const string&in taste, bool is_good=true){
        this.taste=taste;
        this.is_good=is_good;
    }
}
void main(){
    pizza example_pizza("tomatoes", true); //new way to initialize variables!
    speak("I'm taking a bite out of the pizza. It tastes like "+example_pizza.taste+".");
    if(example_pizza.is_good)
        speak("I feel like that was a great snack.", interrupt: false);
    else
        speak("I'm feeling horrible!", interrupt: false);
}
```
A few new things going on here.

Yes, as you may have guessed, classes support functions. They are declared the same way as functions outside of classes, with some bonus fun:
* Constructors (as in the previous example) are called to initialize members of a class. Their declarations have no name, only the return type (the class itself) and arguments.
* The destructor (similar to the constructor) has a ~ at the beginning of its declaration and doesn't have a name either. It is called on an instance of a class just before it is destroyed (in other words, when there are no references to it anymore).
* A class may have an unlimited number of constructors (see previous section on function overloading). However, since destructors do not have any arguments, only one destructor per class is allowed.
* All functions inside classes (including any constructors and destructor) are called \*methods\*.
* All methods have access to a special variable: \*this\*. It points to the instance on which the method is being called.
* You can resolve to instance variables inside a method even without using the `this` pointer (i.e. `is_good` instead of `this.is_good`). I recommend you never do that.

When initializing a variable which is to be an instance of a class, you need to call a constructor. The exception is when there is a default constructor (demonstrated later).

Now, what's with `this.taste`, `example_pizza.is_good`, etc?

In angelscript, . is the indirection operator. In other words it allows you to access variables, properties, and methods belonging to a specific instance.

It is also used for certain primitives like strings and other data structures, which are not considered classes in the typical sense. You may recall we used it to find the length of an array, in their section earlier.

Since our pizza-type variable is called example_pizza, it goes on the left-hand side of the indirection operator. On the right-hand side is the variable whose value we want to retrieve.

#### Class Methods
We briefly touched on methods when discussing classes earlier, but let's explore them a bit more. Methods are simply functions that belong to a class - they define what objects of that class can \*do\*.

The key difference between regular functions and methods is that, as stated above, methods always have access to the special `this` variable.

Here's a practical example:

```
#include "speech.nvgt"

class game_character {
    string name;
    int health;
    int max_health;
    
    // Constructor
    game_character(const string&in character_name, int starting_health = 100) {
        this.name = character_name;
        this.health = starting_health;
        this.max_health = starting_health;
    }
    
    // Method to take damage
    void take_damage(int damage) {
        this.health -= damage;
        if (this.health < 0) this.health = 0;
        speak(this.name + " takes " + damage + " damage! Health: " + this.health);
    }
    
    // Method to heal
    void heal(int amount) {
        this.health += amount;
        if (this.health > this.max_health) this.health = this.max_health;
        speak(this.name + " heals for " + amount + "! Health: " + this.health);
    }
    
    // Method to check if alive
    bool is_alive() {
        return this.health > 0;
    }
}

void main() {
    game_character hero("Alice", 80);
    game_character monster("Goblin", 50);
    
    hero.take_damage(20);
    monster.take_damage(30);
    hero.heal(10);
    
    if (hero.is_alive()) {
        speak(hero.name + " survives the encounter!");
    }
}
```

Notice how each method can access and modify the instance's variables using `this`. Methods are what make objects truly useful - they encapsulate both data and behavior in one package.

For over-achievers, there's much more to explore about methods, including private vs public access, static methods, and advanced method features in the comprehensive object-oriented programming tutorial.

#### Inheritance 
Inheritance is one of the core pillars of object-oriented programming. It allows you to create new classes based on existing ones, inheriting their variables and methods while adding new functionality or modifying existing behavior.

Think of it this way: if you have a general "vehicle" class, you might create more specific classes like "car" and "motorcycle" that inherit from vehicle. Both cars and motorcycles are vehicles, so they share common properties like speed and fuel, but they each have their own unique characteristics too.

In AngelScript, inheritance uses a simple syntax:

```
#include "speech.nvgt"

// Base class
class weapon {
    string name;
    int damage;
    
    weapon(const string&in weapon_name, int base_damage) {
        this.name = weapon_name;
        this.damage = base_damage;
    }
    
    void attack() {
        speak("You attack with " + this.name + " for " + this.damage + " damage!", interrupt: false);
    }
}

// Derived class inheriting from weapon
class sword : weapon {
    bool is_sharp;
    
    sword(const string&in sword_name, int base_damage, bool sharpness = true) {
        super(sword_name, base_damage);  // Call parent constructor
        this.is_sharp = sharpness;
    }
    
    // Override the attack method
    void attack() {
        if (this.is_sharp) {
            speak("You slash with the sharp " + this.name + " for " + (this.damage + 5) + " damage!", interrupt: false);
        } else {
            speak("You swing the dull " + this.name + " for " + this.damage + " damage!", interrupt: false);
        }
    }
    
    // New method specific to swords
    void sharpen() {
        this.is_sharp = true;
        speak("The " + this.name + " has been sharpened!", interrupt: false);
    }
}

void main() {
    weapon basic_club("Wooden Club", 10);
    sword magic_blade("Excalibur", 25, true);
    sword old_sword("Rusty Blade", 15, false);
    
    basic_club.attack();
    magic_blade.attack();
    old_sword.attack();
    
    old_sword.sharpen();
    old_sword.attack();  // Now it's sharp!
}
```

The `: weapon` part tells AngelScript that our `sword` class inherits from the `weapon` class. This means:
* The `sword` class automatically gets all the variables and methods from `weapon`
* We can add new variables (like `is_sharp`) and methods (like `sharpen()`) specific to swords
* We can override inherited methods (like `attack()`) to provide different behavior
* We use `super()` in the constructor to call the parent class's constructor

The power of inheritance becomes evident when you realize that you can treat any sword as a weapon. This means you could have a function that accepts any weapon, and it would work with swords, axes, bows, or any other weapon class you create.

We cover more advanced ways inheritance can be used in the object-oriented programming tutorial.

#### Handles And Null Pointers
A handle is a special type of variable which can be used to store a pointer to an object of a reference type.

Objects of reference types are things like classes, arrays, dictionaries and other complex data structures. Those types which are not reference types are called primitive (or value) types.

If you want to learn more about handles, references, and primitive/reference types in more detail, see the memory management tutorial included in this manual.

Handles are both important and useful for two reasons:

First, they allow you to pass large data structures between functions without copying them. In many cases, a full copy would waste memory.

Second, they allow you to reference objects from multiple points in your code. This has numerous advantages.

Consider, perhaps, a set of teams. The player may be a member of an unlimited number of teams. Each team needs to be able to keep track of its members; handles facilitate that.

A note for advanced programmers: AngelScript has a garbage collector which can deal with circular references. Weak references are available too, but are not always called for - especially not in small projects. More info in the memory management tutorial, but I would be remiss not to make you aware here.

The other distinction between a handle and a regular object is that it Is able to store a value of null. Think of a handle like a hand that can reach out and touch an object. Lots of hands could be touching the same object at the same time, or none at all - and the handle doesn't have to be reaching out for anything. When it isn't reaching out, it has a value of null and we call it a \*null-pointer\*.

When you attempt to use the indirection operator on a handle with a value of null, a \*null pointer access\* exception will be raised. If the exception is not caught, NVGT will safely crash.

To create a handle, proceed the type component of the declaration with an at-sign (@). Like this:
```
object@ ptr;
```
One use-case for null pointers is in a game with a player. Suppose that the game allows the player to pick up a weapon, but there's no guarantee they have one at any given time. In such a situation the use of a handle would allow you to express, and check for, that possibility.

Let's observe. Since this is such a small script, it's fine to take advantage of global variables here.
```
#include "speech.nvgt"
class weapon{
    string name;
    int damage;
    weapon(const string&in name, int damage){
        this.name=name;
        this.damage=damage;
    }
}
void attack(){
    if(current_weapon is null){
        speak("I don't have a weapon right now.", interrupt: false);
        return;
    }
    speak("I attack with my "+current_weapon.name+". I deal "+current_weapon.damage+" damage.", interrupt: false);

}
weapon@ current_weapon;
void main(){
    attack();
    @current_weapon=weapon("sword", 10);
    attack();
}
```
When the handle is set to null, we return from the function early. Otherwise we attack. This means that a null-pointer access exception will never be raised.

You will notice that the default value for a handle is null; it was set automatically for us. This is another distinction between handles and the objects themselves: when declaring a handle, no new object is actually created unless you initialize one.

#### Casting: Implicit and Explicit
In programming, to cast is to convert values between types.

We have already covered the most common form of casting/conversion in AngelScript: implicit.

IN many cases, especially with primitive types, NVGT knows when and how to cast objects; it will be handled behind the scenes.

It does this when (i.e.) concatenating an integer onto a string.

Quick sidenote: primitive type casting is called conversion in AngelScript. Reference type casting is just called casting.

In simple projects you won't need to worry about conversion from reference types to primitive types.

In fact, for classes themselves, your every-day game might not have any need for explicit casts.

When you do, their behavior is very useful, though: explicit casts can return handles, which can be null. If the cast fails (and it might, but we can't know at compile time) you will get a null pointer.

Then, as demonstrated in the previous section, you can check for null and make your game behave differently under that circumstance.

The syntax for explicit casts is:
```
cast<newtype>(value);
```
If casting to a reference type, you probably want to cast to a handle of that type, for clarity if nothing else. This will be demonstrated shortly.

A case in which explicit casting is very useful is when converting parent-class instance handles to child-class instance handles.

The inverse operation will always succeed, and in fact does not necessitate explicit casting. This is easy enough to understand: all apples are fruits.

However, not all fruits are apples. So, casting parent handles to child handles, when they are of the wrong type, safely yields a null pointer.

Let's demonstrate this:
```
#include "speech.nvgt"

// Base class
class vehicle {
    string type;
    int speed;
    
    vehicle(const string&in vehicle_type, int max_speed) {
        this.type = vehicle_type;
        this.speed = max_speed;
    }
    
    void describe() {
        speak("This is a " + this.type + " with max speed " + this.speed, interrupt: false);
    }
}

// Derived classes
class car : vehicle {
    int doors;
    
    car(int max_speed, int door_count) {
        super("car", max_speed);
        this.doors = door_count;
    }
    
    void honk() {
        speak("Beep beep!", interrupt: false);
    }
}

class bicycle : vehicle {
    bool has_bell;
    
    bicycle(int max_speed, bool bell = true) {
        super("bicycle", max_speed);
        this.has_bell = bell;
    }
    
    void ring_bell() {
        if (this.has_bell) {
            speak("Ring ring!", interrupt: false);
        } else {
            speak("This bicycle has no bell", interrupt: false);
        }
    }
}

void main() {
    // Create some vehicles
    car my_car(120, 4);
    bicycle my_bike(25, true);
    
    // Store them as vehicle handles (implicit upcast - always works)
    vehicle@[] garage;
    garage.insert_last(my_car);
    garage.insert_last(my_bike);
    
    // Loop through and try to use them
    for (uint i = 0; i < garage.length(); i++) {
        speak("Vehicle " + (i + 1) + ":", interrupt: false);
        garage[i].describe();
        
        // Try explicit downcast to car@ (handle to a car)
        car@ maybe_car = cast<car@>(garage[i]);
        if (maybe_car !is null) {
            speak("It's a car! Let me honk:", interrupt: false);
            maybe_car.honk();
        }
        
        // Try explicit downcast to bicycle@ (handle to a bicycle)
        bicycle@ maybe_bike = cast<bicycle@>(garage[i]);
        if (maybe_bike !is null) {
            speak("It's a bicycle! Let me ring the bell:", interrupt: false);
            maybe_bike.ring_bell();
        }
    }
}
```
Casting is useful in other places too, particularly when working with dictionaries.

In fact, let's move on to those next. OOP is a huge topic, and you can read more about it in its dedicated tutorial.

However, you now know more than enough to get quite far with it in NVGT.

### Dictionaries (Hash Tables)
In order to keep this tutorial fairly simple, I won't go into the specifics of how dictionaries work under the hood.

To lessen the worries of the more experienced programmer, I will assure you that operations on dictionaries in NVGT have the algorithmic complexity you think they do.

With that random sidenote out of the way, I think I ought to explain what this eccentric little type actually is - and what we do with it.

You can think of dictionaries like containers for data, though unlike arrays, these are unordered.

Instead, you assign keys (which need to be strings) to values of any type.

Then, when you want to retrieve values, you can access them via their keys.

AngelScript has made an odd but ultimately useful decision regarding dictionaries: also unlike arrays, one dictionary can store lots of values of different types.

You could have one single dictionary with a string, an array, an instance of a class, and a whole other dictionary inside.

There are two ways to handle data in dictionaries: with indexing and with methods.

A simple demonstration of both:
```
#include "speech.nvgt"
void main(){
    dictionary dict;
    dict["a"]="b";
    speak("The value of the a key is "+string(dict["a"]), interrupt: false);
    dict.set("c", "d");
    string value_of_c;
    dict.get("c", value_of_c); // Place "into" this variable. See memory management tutorial for how this happens
    speak("The value of the c key is "+value_of_c, interrupt: false);
}
```
There are more methods on dictionaries as well. Some of the common ones are:
* exists(const string&in key): Checks whether any values in this dictionary correspond to this key. True if yes, false otherwise
* void delete(const string&in key): Removes a value from the dictionary, using its key
* void delete_all(): Empties the dictionary
* bool is_empty(): checks whether the dictionary is empty of values. True if empty, false otherwise

#### Looping Through Dictionaries
Just like arrays, dictionaries can be iterated through using a foreach loop. Unlike arrays, the order in which the values will appear is unpredictable.

To demonstrate:
```
#include "speech.nvgt"
void main(){
    dictionary dict;
    dict["Alice"]="Bob";
    dict["Charlie"]="David";
    dict["Eve"]="Frank";
    foreach(auto value, string key: dict)
        speak(key+" likes "+string(value), interrupt: false);
}
```

#### The dictionaryValue Type
As mentioned earlier, dictionaries are able to store multiple types of value. This makes them almost completely unique in AngelScript.

The only other way to store arbitrary types is with something called the `any` type. It is documented, but not in this tutorial.

This is something of a double-edged sword: it's very flexible, but you lose the ability to know what type is coming out.

So, you can basically never implicitly convert or cast.

When you retrieve a value from a dictionary, it will often be of type `dictionaryValue`.

This needs to be cast or converted to another type manually. You can either convert it to a primitive type or use the casting operator to convert it into a reference type (like if it is an array, class instance, or nested dictionary).

Handles to reference types can be held in dictionary values.

However, if you try to explicitly cast and (a) the handle is of the wrong type, or (b) a handle is in fact not inside the dictionaryValue, a null pointer will be returned.

Conversions to primitive types are also possible by calling the constructors of those types. However, if the wrong type is inside the dictionaryValue, an uninitialized variable of your chosen type will be returned.

For some examples of uninitialized values: an empty string, or the integer 0, and so forth.

#### Putting It All Together
Here is a big demonstration of dictionaries that you can run:
```
#include "speech.nvgt"

// Sample class, for reference type demonstration
class item {
    string name;
    int value;
    
    item(const string&in item_name, int item_value) {
        this.name = item_name;
        this.value = item_value;
    }
    
    void describe() {
        speak("Item: " + this.name + " (worth " + this.value + " gold)", interrupt: false);
    }
}

void main() {
    // Create a dictionary with mixed types
    dictionary inventory;
    
    // Store primitive types
    inventory["gold"] = 500;                    // int
    inventory["player_name"] = "Alice";         // string
    inventory["health_percent"] = 0.75;         // double
    inventory["has_map"] = true;                // bool
    
    // Store a reference type (class instance)
    item@ sword = item("Silver Sword", 250);
    @inventory["weapon"] = sword;
    
    // Store an array
    int[] potion_counts = {3, 5, 1};
    @inventory["potions"] = potion_counts;
    
    // Store a nested dictionary
    dictionary stats;
    stats["strength"] = 18;
    stats["agility"] = 14;
    @inventory["stats"] = stats;
    
    speak("=== Retrieving Primitive Types ===", interrupt: false);
    
    // Method 1: Direct conversion using constructors
    int gold_amount = int(inventory["gold"]);
    speak("Gold: " + gold_amount, interrupt: false);
    
    string name = string(inventory["player_name"]);
    speak("Player: " + name, interrupt: false);
    
    double health = double(inventory["health_percent"]);
    speak("Health: " + (health * 100) + "%", interrupt: false);
    
    bool has_map = bool(inventory["has_map"]);
    if (has_map) {
        speak("You have the map!", interrupt: false);
    }
    
    // What happens with wrong type conversion?
    int wrong_conversion = int(inventory["player_name"]);
    speak("Wrong conversion of string to int gives: " + wrong_conversion, interrupt: false);
    
    speak("=== Retrieving Reference Types ===", interrupt: false);
    
    // Cast to class instance handle
    item@ retrieved_weapon = cast<item@>(inventory["weapon"]);
    if (retrieved_weapon !is null) {
        retrieved_weapon.describe();
    } else {
        speak("No weapon found", interrupt: false);
    }
    
    // Cast to array handle
    int[]@ retrieved_potions = cast<int[]>(inventory["potions"]);
    if (retrieved_potions !is null) {
        speak("Potion counts: " + retrieved_potions[0] + " health, " + 
              retrieved_potions[1] + " mana, " + 
              retrieved_potions[2] + " stamina", interrupt: false);
    }
    
    // Cast to dictionary handle
    dictionary@ retrieved_stats = cast<dictionary@>(inventory["stats"]);
    if (retrieved_stats !is null) {
        int strength = int(retrieved_stats["strength"]);
        int agility = int(retrieved_stats["agility"]);
        speak("Stats - STR: " + strength + ", AGI: " + agility, interrupt: false);
    }
    
    speak("=== Demonstrating Failed Casts ===", interrupt: false);
    
    // Try to cast a primitive to a class (will fail)
    item@ failed_cast = cast<item@>(inventory["gold"]);
    if (failed_cast is null) {
        speak("Cannot cast integer to item - got null as expected", interrupt: false);
    }
    
    // Try to cast wrong reference type
    int[]@ wrong_array = cast<int[]>(inventory["weapon"]);
    if (wrong_array is null) {
        speak("Cannot cast item to array - got null as expected", interrupt: false);
    }
    
    speak("=== Using exists() and Safe Access ===", interrupt: false);
    
    // Safe pattern for accessing dictionary values
    if (inventory.exists("weapon")) {
        item@ safe_weapon = cast<item@>(inventory["weapon"]);
        if (safe_weapon !is null) {
            speak("Safely retrieved: " + safe_weapon.name, interrupt: false);
        }
    }
    
    // Check for non-existent key
    if (!inventory.exists("armor")) {
        speak("No armor in inventory", interrupt: false);
    }
    
    // Alternative method using get()
    speak("=== Using get() method ===", interrupt: false);
    
    string player_title;
    if (inventory.get("player_name", player_title)) {
        speak("Retrieved with get(): " + player_title, interrupt: false);
    }
    
    // get() with reference types
    item@ weapon_value;
    if (inventory.get("weapon", @weapon_value)) {
        if (weapon_value!is null) {
            speak("Weapon from get(): " + weapon_value.name, interrupt: false);
        }
    }
}
```
For more comprehensive documentation on dictionaries, see the API reference.
### And That's A Wrap
You now know enough about AngelScript that we can start using it in various fun ways.

The next sections will cover nvgt-specific functions and types. You will learn to play sounds, speak text through screen readers and other kinds of voices, get keyboard input and much more.

## Core NVGT Functionality
On top of AngelScript, NVGT has a powerful and versatile set of capabilities.

For example, if you have played any games built with NVGT, you will undoubtedly be aware of its first-class binaural audio support.

You will learn to take advantage of that soon, as well as a variety of other things.

For those who have used the BGT engine, some things you see here may be very familiar. We have made an effort to create an API which is largely compatible with that of BGT, so that converting your games from one language to the other is as straightforward as possible.

That said, many NVGT objects and functions are either more full-featured or behave in subtly different ways, so you should still read over this.

If you want to know more about converting your games from bgt to nvgt, please see the relevant section in the manual.

### Keyboard Input And The Window
This section will discuss methods for finding out what keys the user has pressed and released.

First thing: in order to accept keyboard input, NVGT will need to open a window.

Windows have names, and the name for your program's window can be anything you like.

Commonly, people will include the version or revision of their games in window titles. This is by no means compulsory, but it is a great way to practice with consts!

Then once you've opened your window, you run a loop that includes a call to wait(), so that you aren't taxing the CPU too much.

In NVGT, wait() has a secondary side effect of updating window state. If you don't use it, your program will hang.

Once you have your simple loop with wait() inside, you can start checking for key presses, releases, and other such things.
A bare-bones example of a window:
```
void main(){
if(!show_window("Window Example 1"))
alert("Critical Error", "Can't show the window. Now crashing. Have a nice day!");
exit();
}
while(true){
wait(5); // 5 is standard, but between 2 and 10 is fine.
if(key_pressed(KEY_ESCAPE))
break; // End of loop - end of program - window closes automatically
}
}
```
New functions here! What do they do?

`bool show_window(const string&in title)`: This opens the window. True on successful creation, false otherwise			

There is a kind of unwritten principle in software and game development, which is that if certain things fail, you ought to just exit completely. Your window refusing to open is definitely one of those things.

It's likely a case no one will ever run into, but if it does come up, best to exit cleanly and safely.

There are two reasons why.

First, you might leave random windowless processes hanging around. Since we're making audiogames, these disembodied processes are probably making noise, and are something of a nuisance to deal with.

Next, if something about the runtime environment is so unspeakably broken that your window can't open, chances are that it isn't game time anyway

`bool key_pressed(int key): actually kind of takes a key_code, but we convert it for BGT compatability. Checks whether the user just pressed a key down this frame. True if so, false otherwise.
