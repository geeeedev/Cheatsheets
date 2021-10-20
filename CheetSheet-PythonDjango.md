cmd         | Meaning/Usage
------------|-------------------------
*args		| represents Non-keyword Arguments as variable(s) <br> a special symbol <br> passing a variable **number of arguments** as a list collection to a function <br> 
```py
 def myFunc(*args):
 	for arg in args:
	 	print(arg)
 
 myFunc('Hello', 'These', 'Are', 'Non', 'Keyword', 'Arguments')
```