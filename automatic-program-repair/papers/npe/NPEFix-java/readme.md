# NPEFix: Automatic Runtime Repair of Null Pointer Exceptions in Java


Link: https://arxiv.org/abs/1512.07423

Year: 2015

Notes: In progress

## Notes:

### I. INTRODUCTION

* Null pointer exceptions (NPEs) is an inherent fragility of software
  in programming languages where null pointers are allowed,
  such as C and Java
* Two wats to handle NPEs:
  1. Avoiding them by using null checks
  2. Handling them at runtime by catching exceptions
* The paper focuses on handling them as exceptions (ii) and provides nine alternative execution "strategies" for handling NPEs at runtime.
* Strategies are categorized into two groups:
  1. The first group is about providing an "alternative value" when a null dereference is about to happen
  2. The second group of strategies is about skipping the execution of the null dereference.
* We implement those alternative execution strategies using code transformation:
  * transformations insert hooks for activating a given strategy at runtime
  * The prototype system is called NPEfix

### II. REPAIRING NULL POINTER EXCEPTIONS AT RUNTIME

* NPEfix technique has two steps:
  1. detecting potentially harmful null dereference at runtime (A)
  2. providing execution semantics alternative to crashing (B)

#### A. Detecting Potentially Null Dereferences
* Detection of harmful NPEs is done in two steps:
  1. Assess if reference to a variable is null each time a variable is going to be dereferenced
    * null dereference != bug: In Java, if null dereference occurs, then NullPointerException is thrown. If an exception is caught up in the call stack, then the program contains a way to handle this error.
    * if null dereference is not caught, then it is a bug since it will cause the program to crash.
      * To detect those uncaughtable harmful null pointer exceptions, we build and maintain a runtime model of the try-catch of the stack (Section III-A)
  2. If a null dereference is detected, then we check if it is caught by the try-catch model

#### B. Repair Strategies

* If a harmful null dereference is detected, there are two options: 
  1. Provide an alternative value
  2. Skip the dereference
* 