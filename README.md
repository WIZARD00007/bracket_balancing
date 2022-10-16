# bracket_balancing

Recently I got a question in the interview to check brackets are balanced or not


     "({)}"     -> balanced
     "([{)}]"   -> balanced
     "}{()[]"   -> not balanced
     "((){}[]"  -> not balanced
     
Most of the people used stack in order to solve this problem, but it doesn't work for all the cases

# Using Stack

```python
def checkBalance(expr):  
    stack = []  
    for char in expr:  
        if char in ["(", "{", "["]:  
            stack.append(char)  
        else:  
  
            # Here we check if the current character is not opening  
            # bracket, then it must be closing.  
            # So stack cannot be empty at this point.  
            if not stack:  
                return False  
            curr_char = stack.pop()  
            if curr_char == '(':  
                if char != ")":  
                    return False  
            if curr_char == '{':  
                if char != "}":  
                    return False  
            if curr_char == '[':  
                if char != "]":  
                    return False  
  
    # Here we check empty stack  
    if stack:  
        return False  
    return True  
  
  
expr = "{(})"  
  
if checkBalance(expr):  
    print("The given string is balanced")  
else:  
    print("The given string is not balanced")
```

## output : The given string is not balanced

### So it does't work in this case.

# My Algorithm

```python
def isBalanced(pattern):
  count=0 #to get index of the bracket #if we use find() or index() it will return index of first occurance
  new_lis=list(pattern)
  open_brack=0
  close_brack=0
  for bracket in pattern:
    if bracket in '{([':
      open_brack+=1
    elif bracket in ']})':
      close_brack+=1
  if open_brack!=close_brack:
    return f"{pattern} is Not Balanced"
  else:
    for bracket in pattern:
      count+=1
      if bracket=="{":
        if "}" in pattern[count:]:
          new_lis.remove("{")
          new_lis.remove("}")
      elif bracket=="[":
        if "]" in pattern[count:]:
          new_lis.remove("[")
          new_lis.remove("]")
      elif bracket=="(":
        if ")" in pattern[count:]:
          new_lis.remove("(")
          new_lis.remove(")")
    if len(new_lis)==0:
        return f"{pattern} is Balanced"
    else:
        return f"{pattern} is Not Balanced"
print(isBalanced("({)}"))
print(isBalanced("([{)}]"))
print(isBalanced("}{()[]"))
print(isBalanced("((){}[]"))
```
## output : 

            ({)} is Balanced
            ([{)}] is Balanced
            }{()[] is Not Balanced
            ((){}[] is Not Balanced
            
### I tried with most of the cases. If you found any false conditions, please let me know.

