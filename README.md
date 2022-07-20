# PythonDecorators

What are decorators?

    We touched on decorators previously, such as @classmethod and @staticmethod. To understand decorators, one must first understand the concept that
    in Python, functions act as variables, they are what is called "first class citizens". You could assign a variable with the memory location of a
    function, delete the function name, and it would still work via the newly set variable as it still points to the memory location of the function,
    ex:

    def hello():
      print("Hello!")

    greet = hello
    del hello

    print(greet) -> outputs "Hello!"
    
    This concept is what allows decorators to operate. In a nutshell, decorators "supercharge" our functions by telling the interpreter that the function
    should have extra features, without modifying its structure.
    
    
Higher Order Functions
    
    Higher Order Functions (HOF) are functions that take another function as a parameter or return a function:
    
    def greet(func):
        func()
        
    def greet2():
        def func():
            return 5
        return func
  
  We have already used HOFs previously, as map() and reduce() are HOFs
  
Decorators
    
    As we previously mentioned, decorators allow us to add extra functionality to a function without altering its structure. Here is an example:
    
    def my_decorator(func):
        def wrap_func():
            print("*****")
            func()
            print("*****")
        return wrap_func
        
    @my_decorator
    def hello():
        print("hello")
        
     hello() 
     ^Outputs :   *****
                  hello
                  *****
                  
   As you can see, we have sucessfully added functionality to our hello() function without modifying its structure. We can reuse the @my_decorator
   on as many functions as we wish.
   
   This works because the interpreter is reading the code as if it were actually my_decorator(hello). This is useful because it helps to simplify
   our code.
   
   This also works with input:
   
    def my_decorator(func):
        def wrap_func(x):
            print("*****")
            func(x)
            print("*****")
        return wrap_func
        
    @my_decorator
    def hello(greeting):
        print(greeting)
        
     hello("Howdy!)  
      ^Outputs :  *****
                  howdy
                  *****
                  
                  
   Decorators can also be set to accept as many parameters or keywords arguments as needed, this is decorator pattern:
   
    def my_decorator(func):
        def wrap_func(*args, **kwargs):
            print("*****")
            func(*args, **kwargs)
            print("*****")
        return wrap_func
        
    @my_decorator
    def hello(greeting, emoji=" ):"):
        print(greeting, emoji)
        
     hello("Howdy!)  
      ^Outputs :  *****
                  howdy ):
                  *****

Why do we need decorators?

    To explain the real world application of decorators, we will examine a custom @performance decorator that will test how fast code runs.
    
    from time import time
    
    def performance(func):
        def wrapper(*args, **kwargs):
            time1 = time()
            result = fn(*args, **kwargs)
            time2 = time()
            print(f"Took {time2 - time1} ms")
            return result
        return wrapper    
        
    @performance
    def long_time():
        for i in range(1000000):
            i * 5
            
    long_time() -> will perform the calculation and also display how long it took to run through the loop
    
Link to Repl.it demonstrating the @performance decorator:
https://replit.com/@AutomationApe/Performance


For more information on decorators:
https://www.programiz.com/python-programming/decorator
            
