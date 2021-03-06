# TypeScript Style Guide

This is the TypeScript style guide that we use internally at Vectorface! It is *semi-reasonable*, but it's more important that we keep a consistent look/feel of our code.


## Table of Contents

  1. [Introduction](#introduction)
  1. [Browser Compatibility](#browser-compatibility)
  1. [Files](#files)
  1. [Indentation](#indentation)
  1. [Line Length](#line-length)
  1. [Quotes](#quotes)
  1. [Comments](#comments)
    1. [Class](#class)
    1. [Inline](#inline)
    1. [Todo and XXX](#todo-and-xxx)
	1. [Commented Code](#commented-code)
  1. [Variable Declarations](#variable-declarations)
  1. [Function Declarations](#function-declarations)
    1. [Anonymous Functions](#anonymous-functions)
  1. [Names](#names)
    1. [Variables, Modules, and Functions](#variables-modules-and-functions)
    1. [Types](#types)
    1. [Classes](#classes)
    1. [Interfaces](#interfaces)
    1. [Constants](#constants)
  1. [Statements](#statements)
    1. [Simple](#simple)
    1. [Compound](#compound)
    1. [Return](#return)
    1. [If](#if)
    1. [For](#for)
    1. [While](#while)
    1. [Do While](#do-while)
    1. [Switch](#switch)
    1. [Try](#try)
    1. [Continue](#continue)
    1. [Throw](#throw)
  1. [Whitespace](#whitespace)
  1. [Object and Array Literals](#object-and-array-literals)
  1. [Assignment Expressions](#assignment-expressions)
  1. [=== and !== Operators](#===-and-!==-Operators)
  1. [Eval](#eval)
  1. [TSLint](#tslint)
  1. [License](#license) 

## Introduction
When developing software as an organization, the value of the software produced is directly affected by the quality of the codebase. Consider a project that is developed over many years and handled/seen by many different people. If the project uses a consistent coding convention it is easier for new developers to read, preventing a lot of time/frustration spent figuring out the structure and characteristics of the code. For that purpose, we need to make sure we adhere to the same coding conventions across all of our products. This will not only help new developers, but it will also aid in quickly identifying potential flaws in the code, thereby reducing the brittleness of the code.

**[top](#table-of-contents)**

## Browser Compatibility
  - Target modern browsers `ie >= 9`

**[top](#table-of-contents)**

## Files
  - All TypeScript files must have a ".ts" extension.
  - Class files should be camel case starting with a capital (ie. MyClassName)
  - All files should end in a new line. This is necessary for some Unix systems.

**[top](#table-of-contents)**

## Indentation
  - Always use tabs for indentation, a single tab should be equal to 4 spaces

**[top](#table-of-contents)**

## Line Length
  - Lines must not be longer than 140 characters. 
  - When a statement runs over 140 characters on a line, it should be broken up, ideally after a comma or operator.

**[top](#table-of-contents)**

## Quotes
  - Use single-quotes `''` for all strings, and use double-quotes `""` for strings within strings.

  ```typescript
  // bad
  var greeting:string = "Hello World!";
  
  // good
  var greeting:string = 'Hello World!';
  
  // bad
  var html:string = "<div class='bold'>Hello World</div>";
  
  // bad
  var html:string = '<div class=\'bold\'>Hello World</div>';
  
  // good
  var html:string = '<div class="bold">Hello World</div>';
  ```

**[top](#table-of-contents)**

## Comments
  - Comments are strongly encouraged. It is very useful to be able to read comments and understand the intentions of a given block of code. 
  - Comments need to be clear, just like the code they are annotating. 
  - Make sure your comments are meaningful. 

The following example is a case where a comment is completely erroneous, and can actually make the code harder to read.

  ```typescript
  // Set index to zero.
  var index = 0;
  ```
    
  - All public functions must have a comment block `/**...*/` using [JSDoc](http://usejsdoc.org/) style comments. 

JSDocs can be interpreted by IDEs for better intellisense. Below is an example of a JSDoc comment block for a function.

  ```typescript
  /**
   * Takes in a name and returns a greeting string.
   * 
   * @param name The name of the greeted person.
   */
  function getGreeting(name:string):string {
      return 'Hello ' + name + '!';
  }
  ```

### Class

  - All classes must have block comments `/**...*/` for all public variables and functions. 
  - All public functions should use [JSDoc](http://usejsdoc.org/) style comments. 
  - Functions need to have a comment explaining what the function does, and all of the input parameters need to be annotated with `@param`. 
  - The class should include a block comment containing the description of the class
  - The constructor should contain a JSDoc comment annotating any input parameters.
  - All methods and variables on a class must have `public` or `private` as a scope.
  - Static methods and variables at the top of the class above instance methods and variables.

  ```typescript
  /**
   * Contains properties of a Person.
   */
  class Person {
      /**
       * Returns a new Person with the specified name.
       * 
       * @param name The name of the new Person.
       */
      public static getPerson(name:string):Person {
          return new Person(name);
      }
      
      /**
       * @param name The name of the new Person.
       */
      constructor(public name:string) { }

      /**
       * Instructs this Person to walk for a certain amount 
       * of time.
       *
       * @param millis The number of milliseconds the Person 
       * should walk.
       */
      public walkFor(millis:number) {
          console.log(this.name + ' is now walking.');
          
          setTimeout(() => {
              console.log(this.name + ' has stopped walking.');
          }, millis);
      }
  }
  ```

**[top](#table-of-contents)**

### Inline

  - Inline comments are comments inside of complex statements (loops, functions, etc). 
  - Use `//` for all inline comments. 
  - Keep comments clear and concise. 
  - Place inline comments on a newline above the line they are annotating
  - Put an empty line before the comment.

  ```typescript
  // bad
  var lines:Array<string>; // Holds all the lines in the file.
  
  // good
  // Holds all the lines in the file.
  var lines:Array<string>;
  
  // bad
  function walkFor(name:string, millis:number) {
      console.log(name + ' is now walking.');
      // Wait for millis milliseconds to stop walking
      setTimeout(() => {
          console.log(name + ' has stopped walking.');
      }, millis);
  }
  
  // good
  function walkFor(name:string, millis:number) {
      console.log(name + ' is now walking.');
      
      // Wait for millis milliseconds to stop walking
      setTimeout(() => {
          console.log(name + ' has stopped walking.');
      }, millis);
  }
  ```

**[top](#table-of-contents)**

### Todo and XXX

`TODO` and `XXX` annotations help you quickly find things that need to be fixed/implemented. 

  - Use `// TODO:` to annotate solutions that need to be implemented. 
  - Use `// XXX:` to annotate problems the need to be fixed. 
  - It is best to write code that doesn't need `TODO` and `XXX` annotations, but sometimes it is unavoidable. 

**[top](#table-of-contents)**


### Commented Code

  - Commented Code should only be used in cases where code will be implemented in the future, but for some reason it is not now.
  - No Commented Code should be left purely because it was the previous implementation or an attempt at a new implementation; the source repository has the full history of changes if a revert is required.
  - If code is to be left around in a commented state, it should be accompanied by a comment (at the beginning of the block of code) that explains why it is still there.
  - Any code that is commented should be done so in `/*...*/` blocks.

**[top](#table-of-contents)**


## Variable Declarations

  - All variables must be declared prior to using them. This aids in code readability and helps prevent undeclared variables from being hoisted onto the global scope. 
  
  ```typescript
  // bad
  console.log(a + b);

  var a:number = 2,
      b:number = 4;

  // good
  var a:number = 2;
  var b:number = 4;
      
  console.log(a + b);
  ```

  - Implied global variables should never be used. 
  - You should never define a variable on the global scope from within a smaller scope.
  
  ```typescript
  // bad
  function add(a:number, b:number) {
      // c is on the global scope!
      c = 6;
      
      return a + b + c;
  }
  ```

  - Use one `var` keyword to define each variable.
  - Declare each variable on a newline.
  
  ```typescript
  // bad
  var a:number = 2,
      b:number = 2,
      c:number = 4;

  // good
  var a:number = 2;
  var b:number = 2;
  var c:number = 4;
  
  // bad
  // b will be defined on global scope.
  var a = b = 2, c = 4;
  ```

## Function Declarations

  - All functions must be declared before they are used.
  - Any closure functions should be defined right after the var declarations.

  ```typescript
  // bad
  function createGreeting(name:string):string {
      var message:string = 'Hello ';

      return greet;

      function greet() {
          return message + name + '!';
      }
  }
  
  // good
  function createGreeting(name:string):string {
      var message:string = 'Hello ';

      function greet() {
          return message + name + '!';
      }

      return greet;
  }
  ```

  - There should be no space between the name of the function and the left parenthesis `(` of its parameter list.
  - There should be one space between the return type, ie `:void`, and the left curly `{` brace that begins the statement body.

  ```typescript
  // bad
  function foo ():void{
      // ...
  }
  
  // good
  function foo():void {
      // ...
  }
  ```

  - The body of the function should be indented 1 tab.
  - The right curly brace `}` should be on a new line.
  - The right curly brace `}` should be aligned with the line containing the left curly brace `{` that begins the function statement.
  
  ```typescript
  // bad
  function foo():string {
    return 'foo';}

  // good
  function foo():string {
      return 'foo';
  }
  ```
  
  - For each function parameter
    - There should be no space between the parameter and the colon `:` indicating the type declaration.
	- There should also be no space between the closing parenthesis `)` and the return type, ie `:string`.

  ```typescript
  // bad
  function greet(name:string):string {
    // ...
  }
  
  // good
  function greet(name:string):string {
    // ...
  }
  ```

**[top](#table-of-contents)**

### Anonymous Functions

  - All anonymous functions should be defined as fat-arrow/lambda `() => { }` functions unless it is absolutely necessary to preserve the context in the function body.
  - All fat-arrow/lambda functions should have parenthesis `()` around the function parameters.

  ```typescript
  // bad
  clickAlert() {
      var element:Element = document.querySelector('div');
      
      this.foo = 'foo';
      
      element.addEventListener('click', function(ev:Event) {
          // this.foo does not exist!
          alert(this.foo);
      });
  }
  
  // good
  clickAlert() {
      var element:Element = document.querySelector('div');
      
      this.foo = 'foo';
      
      element.addEventListener('click', (ev:Event) => {
          // TypeScript allows this.foo to exist!
          alert(this.foo);
      });
  }
  ```

  - There should be a space between the right parenthesis `)` and the `=>`
  - There should be a space between the `=>` and the left curly brace `{` that begins the statement body.

  ```typescript
  // bad
  element.addEventListener('click', (ev:Event)=>{alert('foo');});
  
  // good
  element.addEventListener('click', (ev:Event) => {
      alert('foo');
  });
  ```

  - The statement body should be indented 1 tab.
  - The right curly brace `}` should be on a new line.
  - The right curly brace `}` should be aligned with the line containing the  left curly brace `{` that begins the function statement.

**[top](#table-of-contents)**

## Names

  - All variable and function names should be formed with alphanumeric `A-Z, a-z, 0-9` and underscore `_` characters.

### Variables, Modules, and Functions

  - Variable, module, and function names should use lowerCamelCase.

**[top](#table-of-contents)**

### Types

  - Types should be used whenever necessary.
  - Arrays should be defined as `type[]` instead of `Array<type>`.
  
  ```typescript
  // bad
  var myArray:Array<number> = [];
  
  // good
  var myArray:number[] = [];
  
  // bad 
  var myGrid:Array<Array<number>> = [];
  
  // good
  var myGrid:number[][] = [];
  ```
  - Use the `any` type sparingly, it is always better to define an interface.
  - Always define the return type of functions.
  - Always define the variable type.
  
  ```typescript
  // bad 
  var x = 5;
  
  // good
  var x:number = 5;
    
  // bad
  function toString(someInt:number) {
      return someInt.toString();
  }
  
  // good
  function toString(someInt:number):string {
      return someInt.toString();
  }
  ```

**[top](#table-of-contents)**

### Classes

  - Classes/Constructors should use UpperCamelCase (PascalCase).
  - `Private` and `private static` members in classes should be denoted with the `private` keyword.
  - `Private` and `private static` members should be prefaced with 1 underscore `_`.
  - `Protected` members in classes use the `public` keyword.
  - `Protected` members in classes should have a `@protected` in their **JSDoc**
  - `Protected` members in classes should be prefaced with 2 underscores `__`.

  ```typescript
  class Person {
      private _fullName:string;
      private _firstName:string;
      private _lastName:string;
      /**
       * @protected
       * Speed of the person in m/s.
       */
      public __speed:number = 5; 
      
      constructor(firstName:string, lastName:string) {
          this._firstName = firstName;
          this._lastName = lastName;
          this._fullName = firstName + ' ' + lastName;
      }
      
      private _walkFor(millis:number):void {
          console.log(this._fullName + ' is now walking ' + this.__speed + 'm/s.');
          
          // Wait for millis milliseconds to stop walking
          setTimeout(() => {
              console.log(this._fullName + ' has stopped walking.');
          }, millis);
      }
      
      public toString():string {
          return this._fullName;
      }
  }
  ```

**[top](#table-of-contents)**

### Interfaces

  - Interfaces should use UpperCamelCase.
  - Interfaces should be prefaced with the capital letter I.
  - Only `public` members should be in an interface, leave out `protected` and `private` members.
  
  ```typescript
  interface IPerson {
      firstName:string;
      lastName:string;
      toString():string;
  }
  ```

**[top](#table-of-contents)**

### Constants

  - All constants should use UPPER_SNAKE_CASE.
  - All constant events should use EVT_UPPER_SNAKE_CASE.

**[top](#table-of-contents)**

## Statements

### Simple

  - Each line should contain at most one statement.
  - A semicolon should be placed at the end of every simple statement.
  
  ```typescript
  // bad
  var greeting:string = 'Hello World'

  alert(greeting)
  
  // good
  var greeting:string = 'Hello World';

  alert(greeting);
  ```

**[top](#table-of-contents)**

### Compound

Compound statements are statements containing lists of statements enclosed in curly braces `{}`.

  - The enclosed statements should start on a newline if it's a multi-line statement.
  - The enclosed statements should be indented 1 tab.

  ```typescript
  // bad
  if (condition) { condition = false; alert('Passed!'); }
  
  // good
  if (condition) { 
      condition = false;
      alert('Passed!'); 
  }
  ```
  - The left curly brace `{` should be at the end of the line that begins the compound statement.
  - The right curly brace `}` should begin a line and be indented to align with the line containing the left curly brace `{`.
  
  ```typescript
  // bad
  if (condition)
  { 
      condition = false;
      alert('Passed!');
  }

  // good
  if (condition) {
      condition = false;
      alert('Passed!');
  }
  ```
  
  - **Braces `{}` must be used around all multi-line compound statements**.
  - Compound statements do not need to end in a semicolon `;` with the exception of a `do { } while();` statement.

**[top](#table-of-contents)**

### Return

  - If a `return` statement has a value you should not use parenthesis `()` around the value, unless it helps readability.
  - The return value expression must start on the same line as the `return` keyword.
  
  ```typescript
  // bad
  return 
      'Hello World!';

  // bad
  return ('Hello World!');

  // good
  return 'Hello World!';
  
  // good
  return (override || ((x + 5 < y) && (y < z)));
  ```

  - It is recommended to take a return-first approach whenever possible.
  
  ```typescript
  // bad
  function getHighestNumber(a:number, b:number):number {
      var out:number = b;

      if(a >= b) {
          out = a;
      }

      return out;
  }
  
  // good
  function getHighestNumber(a:number, b:number):number {
      if(a >= b) {
          return a;
      }

      return b;
  }
  ```

  - Always **explicitly define a return type**. This can help TypeScript validate that you are always returning something that matches the correct type.

  ```typescript
  // bad
  function getPerson(name:string) {
      return new Person(name);
  }
  
  // good
  function getPerson(name:string):Person {
      return new Person(name);
  }
  ```

**[top](#table-of-contents)**

### If

  - Always be explicit in your `if` statement conditions when not dealing with any other type other than `boolean`.
  
  ```typescript
  // bad
  function isString(str:any):boolean {
      return !!str;
  }

  // good
  function isString(str:any):boolean {
      return typeof str === 'string';
  }
  ```

Sometimes simply checking falsy/truthy values is fine, but the general approach is to be explicit with what you are looking for. This can prevent a lot of unnecessary bugs.

If statements should take the following form:

  ```typescript
  if (/* condition */) {
      // ...
  }
  
  if (/* condition */) {
      // ...
  } else {
      // ...
  }
  
  if (/* condition */) {
      // ...
  } else if (/* condition */) {
      // ...
  } else {
      // ...
  }
  ```

**[top](#table-of-contents)**

### For

For statements should have the following form:

  ```typescript
  for(/* initialization */; /* condition */; /* update */) {
      // ...
  }
  
  var keys:string[] = Object.keys(/* object */);
  var length:number = keys.length;
  
  for(var i:number = 0; i < length; ++i) {
      // ...
  }
  ```

Object.prototype.keys is supported in `ie >= 9`.

  - Use Object.prototype.keys in lieu of a `for...in` statement.

**[top](#table-of-contents)**

### While

While statements should have the following form:

  ```typescript
  while (/* condition */) {
      // ...
  }
  ```

**[top](#table-of-contents)**

### Do While

  - Do while statements should be avoided unless absolutely necessary to maintain consistency.
  - Do while statements must end with a semicolon `;`

Do while statements should have to following form:

  ```typescript
  do {
      // ...
  } while (/* condition */);
  ```

**[top](#table-of-contents)**

### Switch

Switch statements should have the following form:

  ```typescript
  switch (/* expression */) {
      case /* expression */:
          // ...
          /* termination */
      default:
          // ...
  }
  ```

  - Each switch group except default should end with `break`, `return`, or `throw`.

**[top](#table-of-contents)**

### Try

  - Try statements should be avoided whenever possible. They are not a good way of providing flow control.

Try statements should have the following form:

  ```typescript
  try {
      // ...
  } catch (error:Error) {
      // ...
  }
  
  try {
      // ...
  } catch (error:Error) {
      // ...
  } finally {
      // ...
  }
  ```

**[top](#table-of-contents)**

### Continue

  - It is recommended to take a continue-first approach in all loops.

**[top](#table-of-contents)**

### Throw

  - Avoid the use of the throw statement unless absolutely necessary.
  - Flow control through try/catch exception handling is not recommended.

**[top](#table-of-contents)**

## Whitespace

Blank lines improve code readability by allowing the developer to logically group code blocks. Blank spaces should be used in the following circumstances.

  - A keyword followed by left parenthesis `(` should be separated by 1 space.
  
  ```typescript
  // bad
  if(condition) {
      // ...
  }

  // good
  if (condition) {
      // ...
  }
  ```

  - All operators except for period `.`, left parenthesis `(`, and left bracket `[` should be separated from their operands by a space.

  ```typescript
  // bad
  var sum:number = a+b;
  
  // good
  var sum:number = a + b;
  
  // bad
  var name:string = person . name;
  
  // good
  var name:string = person.name;
  
  // bad
  var item:number[] = items [4];
  
  // good
  var item:number[] = items[4];
  ```

  - No space should separate a unary/incremental operator `!x, -x, +x, ~x, ++x, --x` and its operand.
  
  ```typescript
  // bad
  var neg:number = - a;

  // good
  var neg:number = -a;
  ```
  
  - Each semicolon `;` in the control part of a `for` statement should be followed with a space.
  
  ```typescript
  // bad
  for(var i:number = 0;i < 10;i++) {
      // ...
  }

  // good
  for(var i:number = 0; i < 10; i++) {
      // ...
  }
  ```

**[top](#table-of-contents)**

## Object and Array Literals

  - Use curly braces `{}` instead of `new Object()`.
  - Use brackets `[]` instead of `new Array()`.

**[top](#table-of-contents)**

## Assignment Expressions

  - Assignment expressions inside of the condition block of `if`, `while`, and `do while` statements should be avoided.

  ```typescript
  // bad
  while (node = node.next) {
      // ...
  }
  
  // good
  while (typeof node === 'object') {
      node = node.next;
      
      // ...
  }
  ```

**[top](#table-of-contents)**

## === and !== Operators

  - It is better to use `===` and `!==` operators whenever possible.
  - For `boolean`s only you can use variable-only statements 

  ```typescript
  // bad
  var x:number = 0;
  // some stuff
  if (x) {
      // do something
  }
  
  // good
  var x:number = 0;
  // some stuff
  if (x != 0) {
      // do something
  }
  
  // good
  var x:number = 0;
  // some stuff
  var y:boolean = (x != 0);
  // maybe more stuff
  if (y) {
      // do something
  }
  ```
  
  - `==` and `!=` operators do type coercion, which can lead to headaches when debugging code.
  - It is acceptable to do `==` and `!=` on objects so you do not need to check for `null` and `undefined` in a multi-level object (this could result in a very large if statement).

**[top](#table-of-contents)**

## Eval

  - **Never use eval**
  - **Never use the Function constructor**
  - **Never pass strings to `setTimeout` or `setInterval`**

**[top](#table-of-contents)**

## TSLint

  - Always use a Linter

Linting your code is very helpful for preventing minor issues that can escape the eye during development. We use TSLint (written by Palantir) for our linter.

  - TSLint: https://github.com/palantir/tslint
  - Our [tslint.json](https://github.com/Platypi/style_typescript/blob/master/tslint.json)

## License
(The MIT License)

Copyright (c) 2014 Platypi, LLC

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
