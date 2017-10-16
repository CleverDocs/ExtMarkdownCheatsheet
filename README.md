# ExtMarkdown Cheasheet

This cheatsheet is intended as a quick reference and showcase to **ExtMarkdown**.

ExtMarkdown is an extension to markdown which bring some extra features to [John Gruber's original markdown format](http://daringfireball.net/projects/markdown/). Below are main features given by ExtMarkdown :

## Table of content

- [Operations](Operations)
- Styles
- File Embed
- Value References

## Operations

The first purpose of operation feature is to bring arithmetic operations to a markdown document.

```markdown
You can get an approximative value of pi by dividing 22 by 7.
The results is : **{{(PI) = 22/7}}**
```

### General Structure

Operations are delimited by a double-accolade `{{}}` and are composed by :

- Reference name before the equal `=` sign and must be named with alphanumeric characters only
- The operation, after the equal `=` sign

In this example, `{{PI = 22/7}}`, `PI` is the reference and `22/7` is the operation.

Of course, you can use another reference inside a same operation like this :

```markdown
{{R = 13}}
{{PI = 22/7}}
{{P = 2 * PI * R}}
```

References are case sensisitive.

### Types

#### Result redering

When you want to output a reference, you have to use double-parenthesis like this `((PI))`. Reference must be of course declared no matter where but inside the document.

```markdown
{{PI=22/7}}
You can get an approximative value of pi by dividing 22 by 7.
The results is : **((PI))**
```
This will render :

You can get an approximative value of pi by dividing 22 by 7.
The results is : **3.142857143**

#### Direct result rendering

You can also set the output directly inside the operation by embrace the reference with a parenthesis `{{(PI) = 22/7}}`

```markdown
You can get an approximative value of pi by dividing 22 by 7.
The results is : **{{(PI) = 22/7}}**
```
This will render :

You can get an approximative value of pi by dividing 22 by 7.
The results is : **3.142857143**

In this case, provinding a reference is not mandatory because you don't need to use the variable elsewhere. So, this syntax is correct :

```markdown
You can get an approximative value of pi by dividing 22 by 7.
The results is : **{{() = 22/7}}**
```

You can also write this `{{= 22/7}}` but this will do the operation without outputing it and without setting it inside a reference. So, this is a non-sense.

#### Multiline operations

You can set, inside only one operation, several references.

```markdown
{{
  RADIUS = 13
  PI = 22 / 7
  PERIMETER =  2 * PI * RADIUS
}}
```

The line order doesn't matters.

#### Tables

If you want table to be referenced, you must use bracket delimiters `[]`.

The next structure provides a table :

```markdown
[[FRUITLIST/COL0,COL1,COL2/LINE0,LINE1,LINE2,LINE3,LINE4 =

| Fruits      | How Many | Price |
| ----------- |:--------:|:-----:|
| Apple       | 5        | 5     |
| Bananas     | 2        | 5     |
| Pineapple   | 2        | 10    |
| Total       | =[COL1][LINE1]+[COL1][LINE2]+[COL1][LINE3] | =[COL2][LINE1]+[COL2][LINE2]+[COL2][LINE3] |

]]
```

When you declare a table inside ExtMarkdown document, you must provide inside the first line :

- The table reference (On the above example : `FRUITLIST`)
- Every column reference after the `/` (On the above example, there is 3 columns `COL0`, `COL1`, `COL2`)
- Every lines references after another `/` (On the above example, there is 3 columns `LINE0`, `LINE1`, `LINE2`, `LINE3`, `LINE4`)

And after that, you have the table in classic markdown format.
Note that if your column and line references don't match with your provided table, you will get an error.

Inside a cell, you can set operations. Just start the cell value with `=`. You can set only one operation per cell.

Inside a table you can reference :

- another cell inside the current table (For example, this reference `[COL1][LINE3]` will find the colum referenced by `COL1` and the line referenced by `LINE3`)
- a cell inside another table inside the document, using the table reference `FRUITLIST[COL1][LINE3]`
- another non cell reference

Outside a table, you can use a cell reference by providing table, column and line references `FRUITLIST[COL1][LINE3]`.

### Operators

| Operators      | Symbols | Example |
| -------------- |:-------:|:-------:|
| Addition       | +       | 10 + 14 |
| Soustraction   | -       | 10 - 14 |
| Multiplication | *       | 10 * 14 |
| Division       | /       | 10 / 14 |

All other operators are represented by functions. Get a full list in [this page](Defined-Functions).

### Errors

Operation errors, if the rendered, will result by a print of a double question mark (??). If there is no render, the error will not be outputed.

- If a variable you attempt to show don't exists or is a result of an operation with error, it will be replaced by a double question mark (??).
- If there is a syntax error in operation that you are printing the result, you will get double question mark (??) instead of the result

### Not another meta-language

**ExtMarkdown's Operations is not another language or meta-language.** It doesn't behaves like a programmatic languages.

#### Reference are not variables

If you try to set a reference more than once. Your reference will be invalid and you'll get an error.

#### Line/Operation order doesn't matters

There's is no chronology logic. In the 2 above examples, `PERIMETER` will always have the value `33.647058824`.

```markdown
{{
  RADIUS = 13
  PI = 22 / 7
  PERIMETER =  2 * PI * RADIUS
}}
```

```markdown
{{
  PERIMETER =  2 * PI * RADIUS
  PI = 22 / 7
  RADIUS = 13
}}
```

#### Why the hell ???

We understand that this is a little bit confusing for users familiar with programming languages. But the idea behind ExtMarkdown is to mimic spreadsheet behavior and not programming languages.

With tools like Google SpreadSheet and Ms Excel, you can set an operation inside a cell on bottom of your table and use his value on top. It would not be possible if ExtMarkdown's operations behaves like a programmatic language.
