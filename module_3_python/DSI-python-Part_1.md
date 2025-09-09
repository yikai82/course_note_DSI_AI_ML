<p align="center">
  <img src="[insert XXX IMAGE URL]" alt="XXX Logo" width="120">
</p>     

# 

<h1 align="center">
  DSI AI/ML Course <br>
  Module 3 – 🐍 Python - Part 1</h1>

<p align="center">
  <!-- [INSERT TEXT]<br> -->
  <a href="#key-note-and-important-concept">Key Notes</a> •
  <a href="#2-basic-string-operation">String Formatting</a> •
  <a href="#3-logical-operators-and-or-not">Logical Operators</a> •
  <a href="#other-references">References</a>
</p>

---
## The content below was covered during WEEK 1 of the Python Live session.
 
### Content  
* [Key Note and Important Concept](#key-note-and-important-concept)  
* [1. Basic Arithmetic and Comparison Operation](#1-basic-arithmetic-and-comparison-operation)
* [2. Basic String Operations](#2-basic-string-operation)  
* [3. Logical Operators: `and`, `or`, `not`](#3-logical-operators-and-or-not)  
* [4. If statement](#4-if-statement)  
* [5. Functions and Methods](#5-functions-and-methods)

<!-- * **[Situation Room 🚨](#situation-room-)**  <--- got stuck? ⚓😣 check here first  -->


<!-- **![BONUS](https://img.shields.io/badge/BONUS-FFB6C1)** **![Jupyter Lab](https://img.shields.io/badge/_Jupyter_Lab-E65C00)**  
It also include my little experiment of trying everything in the **Jupyter Lab**  -->  

---
## System  

<div align="left">
  <div style="margin: 2px 0;">
    <img src="image/Linux2.svg" alt="Linux" width="50" style="vertical-align: middle; margin-right: 6px;">
    <span style="vertical-align: middle;">Kubuntu-T2 24.04.2 LTS</span>
  </div>
  <div style="margin: 2px 0;">
    <img src="image/Noble.svg" alt="Noble" width="50" style="vertical-align: middle; margin-right: 6px;">
    <span style="vertical-align: middle;">Codename: Noble</span>
  </div>
</div>  

Release:	24.04 LTS  
Kernel Version: Linux 6.14.0-1-t2-nob



---
## Key Note and Important Concept:
> [!NOTE]  
> 1. Jupyter Notebook is not behaving 😵‍💫 and you want a refresh start? Look for **`Clear All Outputs`** and **`Restart ➡️ Kernel`**.  
> 2. An empty string = `""`. **No space!**  
> 3. The best way to play with code: use comment shortcut `ctrl +/` to add/remove specific lines of code to see the response.  
> 4. **Docstrings**: `'''a lot of text'''`. ---> see section xyz 
> Escape sequence: `\n`, `\'`, `\"`,`\\`.  
> `If statement`: **else** needs if, but if does not need else.  
> 5. **`in`** operator ---> See [Example]() 

> [!IMPORTANT]  
> 1. Pay attention to the data type.  
> 2. Python string is **0 index** [Start with 0], so any function requiring **index** will not work ⛔.  
> 3. Any empty string("") is treated as **`False`**, while any non-empty string(" ","xyz", etc.) is treated as **`True`**.  
> 4. F string: `f"{var1},{var2}"`---> [See Section 2.3](#23-stringsstrings-formatting).  
> 5. **Boolean**:   
    - `and`: returns the 1st false or the last truthy.  
    - `or` : returns the 1st truthy or the last false.  
> 7. You don't need `if...return True...else: return False` if you are already using comparison operators that will return True/False automatically---> [See Section 4.1](#41-an-example-of-unnecessary-ifelse)   

> [!WARNING]  
> When working with logical operators `and`, `or`, and `not`, it is important to ensure using Boolean values so the function (or the model) is clear and has a more consistent behavior --> [See Section 3](#3-logical-operators-and-or-not)
>    

🚨 Cannot access Jupyter Notebook in VS Code? Try Google Colab

**Disclaimer**: *I have made every effort to ensure the accuracy of this document, but errors may still be present. Please proceed with caution.*

<sub>[↥ back to top](#)</sub> 

---
## 1. Basic Arithmetic and Comparison Operation

### 1.1 Calculation and Basic Functions 

```python
10/3      # /   normal division
10//3     # //	Integer division (always rounds down)
10&3      # %	  Modulo or remainder
10**3     # **	Exponentiation
float()
int()
round()
abs()
```
  
### 1.2 Comparison Operation  

  | Operator | Description |
  | --- | --- |
  | `>` | Greater than |
  | `>=` | Greater than or equal to |
  | `<` | Less than |
  | `<=` | Less than or equal to |
  | `==` | Equal to |
  | `!=` | Not equal to |

### 1.3 The hierarchy with logical operators:  

  Arithmetic and comparison operator s are evaluated first and Boolean operators are evaluated after arithmetic and comparison operators:  

  | Order | Operator | Description |  
  |---|---|---|  
  | 1 | `**` | Exponentiation |  
  | 2 | `-`| Negation |  
  | 3 | `*`, `/`, `//`, `%` | Multiplication, division, integer division, and modulo |  
  | 4 | `+`, `-` | Addition and subtraction |  
  | 5 | `<`, `<=`, `>`, `>=`, `==`, `!=` | Less than, less than or equal to, greater than, greater than or equal to, equal, not equal |  
  | 6 | `not` | Not |  
  | 7 | `and` | And |  
  | 8 | `or` | Or|


<sub>[↥ back to top](#)</sub>

---
## 2. Basic String Operation 

### 2.1 A few simple examples:

```python
'hello' + ' ' + 'world'   # add string together
'haha'*3                  # return 'hahahahaha'

print('hello') 
id(var)                   # call out the location of a specific variable
len('string')             # output the length of the string
sorted('string')          # sorted the string alphabetically 



text = 'a_string'[0:4]    # output the position 0 and 3 (not including 4) from the string
text[0:1]                 # output the position 0 and not including 1 from the string
text[0:9:2]

# String method
'string'.upper()
'string'.lower()
'This string is unusual'.count('e') # count letter "e"
'file_name.csv'.endswith('.csv')
'long file name with spaces.csv'.replace(' ', '_')  # replace space with underscore

``` 

<sub>[↥ back to top](#)</sub>

---
### 2.2 Escape Sequence

  | Escape sequence | Description        |
  |-----------------|--------------------|
  | \\'             | Single quote       |
  | \\"             | Double quote       |
  | \\\\            | Backslash          |
  | \\t             | Tab                |
  | \\n             | Newline            |
  | \\r             | Carriage return    |


### 2.3 Strings/Strings Formatting

```python
## String formatting examples

# Example 1:
first_name = 'Ada'; last_name = 'Lovelace'
'Ada Lovelace\'s initials are {}. {}.'.format(first_name[0], last_name[0])
f'Ada Lovelace\'s initials are {first_name[0]}. {last_name[0]}.'

# Example 2: 
'My favourite veggie is {}'.format('lettuce')
veggie = 'lettuce'; f"My favourite veggie is {'veggie'}"

# Example 3:
text = 'a_string'
t1 = text[0]
t2 = text[1]
t3 = text[0:9:2]
print('{}, {}, {}'.format(t1,t2,t3))  # output method 1
f"{t1}, {t2}, {t3}"                   # outpur method 2  

``` 

### 2.3 Docstring

1. A docstring (short for documentation string) is a special string literal you put inside a function, class, or module to explain what it does. It’s written using triple quotes (""" ... """ or ''' ... '''). Help() or IDEs can display them.

Example: 
```python
def c_to_f(degrees_c):
    """Convert degrees from Celsius to Fahrenheit"""
    degrees_f = (9 / 5) * degrees_c + 32
    return degrees_f


# Enter c_to_f in help()
help(c_to_f)

# Return
Help on function c_to_f in module __main__:
```

<sub>[↥ back to top](#)</sub>

---
## 3. Logical Operators: `and`, `or`, `not` 

### 3.1. **`and`** operator: returns the **first falsy value** encountered or the **last truthy value** if all operands are true.

Copy-paste the following code into Jupyter notebook to see the difference 


```python

# Example 1: 
is_winter = "True"  # non-empty string so it is considered a True (bool)
is_cloudy = True    # True (bool))

is_winter and is_cloudy     # True
is_cloudy and is_winter     # "True" 

# Example 2: 
my_pet = 'dog'    # non-empty string so it is considered True (bool)
xindi_pet = 'cat' # non-empty string so it is considered True (bool)

my_pet and xindi_pet        # 'cat' 
xindi_pet and my_pet        # 'dog'

# Example 3
day_of_week = 'Wednesday' # non-empty string so it is considered True (bool)
month = ''  # empty string so it is considered False (bool)
            # pply with month by input anything

month and day_of_week
```

### 3.2 **`or`** operator: returns **the first truthy** value encountered or **the last falsy** value if all operands  

  - Use the code above to experiment it by replacing `and` to `or` 
  - [The hierarchy with logical operators](#13-the-hierarchy-with-logical-operators)  


<sub>[↥ back to top](#)</sub>

---

## 4. If statement

### 4.1 An example of unnecessary if/else

```python
def test_a_is_bigger(a, b):
    if type (a) == str or type (b) == str:  
        print("you cannot feed me with strings, I dont eat those.\n"
              "you can try feed me with True of False 😎")                  
    
    else:   
        if a > b:     ### Not the best way becasuse "a > b" will return True/False >>>> 
            return True          
        else:                   
            return False        
```

### 🔨 fix the 4.1

```python
def test_a_is_bigger(a, b):
    if type (a) == str or type (b) == str:  
        print("you cannot feed me with strings, I dont eat those.\n"
              "you can try feed me with True of False 😎")                  
    
    else:   
        return a > b               
```
### 4.2 if...elif...else

👉 Check out my python [if logic play book](/module_3_python/python_if_logic_play_book.ipynb)

```python
def test_a_int_and_bigger_yes(a, b, int_check):
    
    if int_check == True or "Yes": ##### -----------------> Play Spot 1: replace [or "Yes"] to other boolean opearator 
        if type(a) == int: 
            print('the first entry is an interger')
            if a > b: print('the first number is bigger')
                              
            else: print('the first number is not bigger than the second number')
            
        else: print('the first entry is not an interger, Calculation Stop!')

    ##### -- Play spot 2: Manually removing and adding back the follow block using ctrl + / in the coding area ----- #####
    elif int_check == False: ###### --------------------> Play Spot 3:Swich elif to if? 
        print('setting int_check == False')

    ##### -- End of the Play Spot 2 ------------------------------------------------------------- #####
    else: print('Hey! you reach the 1st else statement: how did you find me? 🤪')
```
---
## 5. Functions and Methods

### 5.1 Function Creation:  
1. Syntax:  
  `def` Function_name(argument_1, argument_2,.....):
    var1 = 
    var2 = 
    `return` result

Example: 

```python

def c_to_f(degree_c):
    degree_f = (9/5) + degree_c + 32
    return degree_f

``` 

<sub>[↥ back to top](#)</sub>

---
## Other Common Build-In Function
1. `input()`: it will require user to input a variable for the function


2. Type Casting
```python
int()
float()
str()
list()
tuple()

```



<sub>[↥ back to top](#)</sub>

<!-- ---
## Situation Room 🚨


<sub>[↥ back to top](#)</sub> -->

---
### 📚 References:
