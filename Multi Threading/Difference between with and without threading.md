without:
so when we have a program which has two function calling inside it ,the first function
will be executed, only the second program will we executed when the first one is fully completed.

with:
both functions(refer the code) execute parallel without the order of the code. the main thread does not know when the other threads are going to finish so that we use "threadname.join()" to finish.

