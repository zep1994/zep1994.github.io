---
layout: post
title:      "Arrays! Let's Take a Closer Look"
date:       2018-02-28 22:20:51 +0000
permalink:  arrays_lets_take_a_closer_look
---


Imagine trying to create a list of names and and sitting there typing put  `name1 = "Jon", name2 = "Jan"` and so on. This list could get pretty big and would be a pain to type. That is what makes arrays so great. This can store all of that information, in this case the names. Let's create an with a couple names. 
```
names = ["Jon", "Jan"]
```
Let's say we forgot someone! Oops! Let's add them. 
```
names << "Bob"
```
Now our array contains three names with Bob now on the list. But let's say we want to pick a name from our list.
We can call on a specific name using it's index. If we wanted to call on Jan, I can call on Jan using,
```
names[1]
```
Now you might be wondering why I used a 1, intead of a 2. This is because in Computer Science you always start counting at 0. You can change yourself by adding a +1, but that is for another blog. 
 
 Once you have created the list of names, you want to make sure that you have not missed anyone and that you got everyone's name spelled correctly. To do this we want to iterate over the names, which we can do like this:
```
names.each do |name|
    p name
end

```

When we can print the array by simply calling a method, this saves us a lot of time. That is what arrays do, they save us a lot of time. They are like baskets, they can store a bunch of peaches. Arrays do have there limitations, but there are things like hashes for that. Arrays are super useful for things that are similar to each other, like names or peaches. There is a lot more that can be done with arrays that I did not cover here, but it makes for great fun to look up different ways to use them.
