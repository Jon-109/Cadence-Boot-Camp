# Chapter 2 Day 3 Quest Answers

## 1. In a script, initialize an array (that has length == 3) of your favourite people, represented as Strings, and log it.

![Screen Shot 2022-04-29 at 2 29 14 PM](https://user-images.githubusercontent.com/104539205/166057007-1fbec55c-ead4-43a7-a8a1-c70d2be7be0a.png)
![Screen Shot 2022-04-29 at 2 29 30 PM](https://user-images.githubusercontent.com/104539205/166057077-e6cab00a-99b2-4498-aeac-9cac6986f6b4.png)
![Screen Shot 2022-04-29 at 2 29 38 PM](https://user-images.githubusercontent.com/104539205/166057129-8452dadb-c48a-4c38-a182-aa6a5d596b0d.png)

## 2. In a script, initialize a dictionary that maps the Strings Facebook, Instagram, Twitter, YouTube, Reddit, and LinkedIn to a UInt64 that represents the order in which you use them from most to least. For example, YouTube --> 1, Reddit --> 2, etc. If you've never used one before, map it to 0!

![Screen Shot 2022-04-29 at 4 30 02 PM](https://user-images.githubusercontent.com/104539205/166071701-5ff3551f-1e01-40d0-9fbb-872a8c4bb928.png)
![Screen Shot 2022-04-29 at 4 30 27 PM](https://user-images.githubusercontent.com/104539205/166071731-4a1262ab-fbf6-4cea-97dd-331a80939103.png)
![Screen Shot 2022-04-29 at 4 30 37 PM](https://user-images.githubusercontent.com/104539205/166071749-5bb76672-1d41-481b-90f8-86846d1e4891.png)

I wanted to be extra and create a function to print it just to practice a bit I know its not the most efficient but oh well for now if it works it works

## 3. Explain what the force unwrap operator ! does, with an example different from the one I showed you (you can just change the type).

In order to understand what the **force unwrap operator (!)** does, we must first understand what **optionals (?)** do in Cadence. 

**Optional types** are declared on variables by placing a **"?"** after the variable type when declaring a variable as shown in the examples below. 

```cadence

let favNum: Int? = nil
//here I declared an optional String type on a variable called favNum with an initial value of "nil"

let favNum: Int? = 3
//here I declared an optional String type on a variable called favNum with an initial value of 3 

let favNum: Int? = "Dwight" 
//here I declared an optional String type on a variable called favNum with an initial value of "Dwight"
```

The **"?"** indicates that the value of the variable must be the type we want (in this case "String") or "nil" (which means there is no value). Otherwise, the program will abort.

Since the first example has an intial value of "nil" there will not be any compiling errors.

Since the second example has an intial value of 3 and 3 is a "Int" type there will not be any compiling errors.

Since the third example has an intial value of "Dwight" which is an "String", not a "Int" the program will abort. The reason being is because there is an optional Int type declared on these 
variables which means the value of the variables has to be the "Int" or "nil." Since the third example has a variable type "String", that is why the program will abort. 

So optional types basically is the program saying the type better be exactly what we want or nothing at all, or else I'm not running this program.

Either the optional type we want.. or nil ... or abort

What the **force unwrap operator !** does is it returns the value of an optional type if its the type we want, and then it also removes the optional type. 
However, if the optional is nil the program will abort. 
Essentially the force unwrap operator is not a fan of the nil scenario when declaring optional types.

Either the optional type we want and remove the optional type.. or abort


## 4. Using this picture below, explain...
<img width="982" alt="Screen Shot 2022-05-01 at 4 11 15 PM" src="https://user-images.githubusercontent.com/104539205/166164788-7f0a1518-47fa-45f6-835a-1a6252db21a8.png">

### -What the error message means

The error message states "mismatched types. expected String, got String?"

The message is indicating that the expected return value is a String, but instead an optional String type is being returned.

### -Why we're getting this error

This is the case because we know that when elements are pulled from dictionaries in Cadence, the value is returned as an optional type.

### -How to fix it

We can fix this error by placing an force unwrap operator (!) after the return statement to unwrap the optional type and return the actual value type.

```cadence
return thing[0x03]!
```
