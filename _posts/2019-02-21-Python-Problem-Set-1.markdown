**Problem 1**

Assume s is a string of lower case characters.

Write a program that counts up the number of vowels contained in the string s. Valid vowels are: 'a', 'e', 'i', 'o', and 'u'. For example, if s = 'azcbobobegghakl', your program should print:

```Number of vowels: 5```


__Pseudo code:__ 

> set starting point for variable vowels to 0

> for each letter in the given string,
>> For each letter in a string of all vowels ‘aeiou’,
>>> check if the current letter is equal to the current vowel 
>>>> If it is equal, add 1 to the vowels variable

> Print the number of vowels counted

```
vowels = 0
for letter in s:
    for vowel in 'aeiou':
        if letter == vowel:
            vowels += 1
print("Number of vowels: " + str(vowels))
```

___

**Problem 2**

Assume s is a string of lower case characters.
Write a program that prints the number of times the string 'bob' occurs in s. For example, if s = 'azcbobobegghakl', then your program should print

```Number of times bob occurs is: 2```


__Pseudo code:__

> Set starting point for number of bobs in string to 0

> Until the variable s is equal to and empty string ‘ ’, check if the first 3 letters of variable s are equal to “bob” 
>> if they are, add 1 to bobs variable 
>>> Then update the s variable, deleting the first character from the string

> When s variable is an empty string, print out the number of times ‘bob’ occurred 

```
bobs = 0
s = 'azcbobobegghakl'

while s != '':
    if s[0:3] == 'bob':
        bobs += 1
    s = s[1:]
print("Number of times bob occurs is: " + str(bobs))
```

___


**Problem 3**

Assume s is a string of lower case characters.

Write a program that prints the longest substring of s in which the letters occur in alphabetical order. For example, if s = 'azcbobobegghakl', then your program should print

```Longest substring in alphabetical order is: beggh```

In the case of ties, print the first substring. For example, if s = 'abcbcd', then your program should print

```Longest substring in alphabetical order is: abc```


__Pseudo code:__

Set num to start at 0

> start a loop that will stop when num is equal to the length of s + 1
>> in the beginning of the loop reset temp to s 
>> start a loop that will stop when temp is an empty string
>>> go through all the letters in temp and compare to the last one
>>>> if it is, set variable alphabetical to False 

>>> if variable alphabetical is False 
>>>> if the current is string’s length is greater than then the current substring 
>>>>> then set the substring to the current string 

>>> Remove the first character from temp

>> add 1 to num and continue loop

> print the longest substring in alphabetical order 

```
substring = ''
temp = s 
num = 0
while(num < len(s) + 1): 
   temp = s
   while(temp != ''):
           last = ''
           alphabetical = True
           for letter in temp[:num]: 
               if letter < last:
                   alphabetical = False
               last = letter
           if alphabetical == True:
               if len(temp[:num]) > len(substring):
                   substring = temp[:num]
           temp = temp[1:]  
   num += 1
print("Longest substring in alphabetical order is: " + substring)
```
