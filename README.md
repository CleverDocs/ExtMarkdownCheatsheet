# ExtMarkdown Cheasheet

This cheatsheet is intended as a quick reference and showcase to **ExtMarkdown**. 

ExtMarkdown is an extension to markdown which bring some extra features to [John Gruber's original markdown format](http://daringfireball.net/projects/markdown/). Below are main features given by ExtMarkdown :

## Table of content

- [Operations](Operations)
- Styles
- File Embed
- Value References

## Operations

The first purpose of operation feature is to bring arithmetic operations to a markdown document. But you will see that you can use variables like in programming languages. 

### Delimiters

Operations are delimited by a double-accolades `{{}}` :

```markdown
You can get an approximative value of pi by dividing 22 by 7. 
The results is : **{{22/7}}**
```

This will render : 

You can get an approximative value of pi by dividing 22 by 7. 
The results is : **3.142857143**

### Operators

| Operators      | Symbols | Example |
| -------------- |:-------:|:-------:|
| Addition       | +       | 10 + 14 |
| Soustraction   | -       | 10 - 14 |
| Multiplication | *       | 10 * 14 |
| Division       | /       | 10 / 14 |

All other operators are represented by functions. Get a full list in [this page](Defined-Functions).

### Variables and assigned variables

Like with programmation languages, you can use variables in operations.
Variables can be assigned inside an operation :

```markdown
{{ R = 13 }}
```

Or assigned by a bracket after the operation (useful if you are in line) : 

```markdown
{{ 10 + 3 }}(R)
```

When the variable exists, you can show it like this : 

```markdown
The circle have **{{ R }}** radius.
```

This will render : 

The circle have **13** radius.

### Inline and Multiline

You can use single operation and display the result immediately as the exemple above; or you can do complex operation separately with the use of variables and print variables : 

```markdown
**Radius and Perimeter**
{{
    R = 13
    PI = 22 / 7
    P =  2 * PI * R
}}
If the radius is {{ R }}, the perimeter is **{{ P }}**
```

This will render : 

**Radius and Perimeter**
If the radius is 13, the perimeter is **81.714285718**

### Render 

If you operation do an internal assignment, in other terms, if you use the sign equal "=", your result will not be rendered. 

This will show nothings :

```markdown
{{
    R = 13
    PI = 22 / 7
    P =  2 * PI * R
}}
```

In other hand, if not, and probably, you operation is inline but not necessarily, the result will be printed :

```markdown
The perimeter is **{{ 2 * (22 / 7) * 13 }}**
```

This will render : 

The perimeter is **81.714285718**

### Errors

Operation errors, if the rendered, will result by a print of a double question mark (??). If there is no render, the error will not be outputed.

- If a variable you attempt to show don't exists or is a result of an operation with error, it will be replaced by a double question mark (??).
- If there is a syntax error in operation that you are printing the result, you will get double question mark (??) instead of the result

### Complex Structures

#### Conditions

    @TODO
    
#### Loop

    @TODO

#### Functions

    @TODO