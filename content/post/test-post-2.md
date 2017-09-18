---
author: Colman Mbuya
date: "2017-09-18T10:54:24+02:00"
title: Test Post 1234
highlight: true
draft: false
slug: "Test Post 1234"
tags: ["security","blog","post"]
authoravatar: "images/author_cm.png"
image: "images/security_locks.jpg"
comments: false     # set false to hide Disqus comments
share: true        # set false to share buttons
---


### **Introduction**

This is a test post.

Here's some code ```html test123```:
Test <a class="bluetext" href="https://blog.gidzero.com">Link Text</a>
Bold <strong>test</strong>

```html
<!DOCTYPE html>
<html lang="en">
<head>

<script>
	// Just a lil’ script to show off that inline JS gets highlighted
	window.console && console.log('foo');
</script>
<meta charset="utf-8" />
<link rel="shortcut icon" href="favicon.png" />
<title>Prism</title>
<link rel="stylesheet" href="style.css" />
<link rel="stylesheet" href="themes/prism.css" data-noprefix />
<script src="prefixfree.min.js"></script>

<script>var _gaq = [['_setAccount', 'UA-33746269-1'], ['_trackPageview']];</script>
<script src="https://www.google-analytics.com/ga.js" async></script>
</head>
```

```python
#!/usr/bin/python
#
# Generate valid South African ID numbers
# converted from http://knowles.co.za/generating-south-african-id-numbers/
#
# usage: ./zaidnum.py <date of birth (YYMMDD)> <0/1 female/male> <0/1 foreign/citizen>
#
# Some examples:
#
# ./zaidnum.py 801212 1 0
# ./zaidnum.py 751002 0 1


import re, random, math, sys

def generateLuhnDigit(inputString):
    total = 0
    count = 0
    for i in range(0,len(inputString)):
        multiple = count % 2 + 1
        count += 1
        temp = multiple * + int(inputString[i])
        temp = math.floor(temp / 10) + (temp % 10)
        total += temp

    total = (total * 9) % 10

    return int(total)

def getRandom(range):
    return int(math.floor(random.random() * range))

def generateID(dob, male, citizen):
    if not re.match("[0-9][0-9][0-1][0-9][0-3][0-9]",dob):
        return "Please check your date of birth string."

    gender = getRandom(5) + (5 if male == 1 else 0)
    citBit = -citizen+1
    rand = getRandom(1000)

    if rand < 10:
        rand = "00" + str(random)
    elif rand < 100:
        rand = "0" + str(random)

    total = "" + dob + str(gender) + str(rand) + str(citBit) + "8"
    total += str(generateLuhnDigit(total))
    return total

if len(sys.argv) != 4:
    print """usage: ./zaidnum.py <date of birth (YYMMDD)> <0/1 female/male> <0/1 foreign/citizen>

Some examples:

./zaidnum.py 801212 1 0
./zaidnum.py 751002 0 1
          """
    sys.exit()

dob = sys.argv[1]
male = int(sys.argv[2])
citizen = int(sys.argv[3])

print generateID(dob, male, citizen)
```

> This is another way to display some text.

This some other text format ```layouts/```
