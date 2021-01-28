---
template: post
title: "How to sort list using other sorted lists in C# "
slug: /posts/sort-list-using-other-list-linq
draft: false
priority: 0
date: 2020-09-02T03:58:04.860Z
description: This is a common scenario that we face while working. We want to
  sort the list based on the different value of its some of the properties. I
  have explained how to sort List based on other sorted lists in c# using LINQ
category: programming
tags:
  - csharp
  - linq
  - sorting
  - list
  - dotnet
  - asp
  - cs
  - microsoft
---
This is a common scenario that we face while working. We want to sort the list based on the different value of its some of the properties. We can achieve this by iterating through the list and putting several conditional statements. However, It might be hectic if we want to sort the list based on more than one property with multiple values for each property.

![sorting list](/media/sort.jpg "Sorting")

**Image Courtesy: Google** 

LINQ is a life saviour in such a situation and can save our day. We can achieve the same using very minimal lines of code. We will define the lists for the properties through which we want to sort the array and assign the expected value in the sorted order. Then we will use LINQ to iterate and sort the main list.

Here is the link to the fiddle for working [example](https://dotnetfiddle.net/cFQUGA).

Let's start by creating a model class for our example.



```csharp
public class Student {
	public string name {get; set;}
	public string standard { get; set;}
	public string section {get; set;}
	public int rollNumber {get; set;}
}
```

Each student will have a name along with other information such as the standard they are studying on, section and their roll number.

Let's create a generic list of our students.

```csharp
List<Student> students = new List<Student>(){
			new Student {name ="Bob", standard = "Third", section ="A", rollNumber=10},
			new Student {name ="Smith", standard = "Second", section ="B", rollNumber=5},
			new Student {name ="Tylor", standard = "first", section ="A", rollNumber=1},
			new Student {name ="Jack", standard = "Third", section ="A", rollNumber=8},
			new Student {name ="Penny", standard = "second", section ="B", rollNumber=4},
			new Student {name ="Diana", standard = "First", section ="A", rollNumber=1},
			new Student {name ="Selena", standard = "First", section ="B", rollNumber=3},
            new Student {name ="Elon", standard = "Second", section ="A", rollNumber=1},
			new Student {name ="Harry", standard = "Second", section ="B", rollNumber=1},
		};
```

Suppose we want to order the students based on their standard first followed by section and rollNumber respectively in the specific order of their value. For that, let's create a different list with the value in sorted order. rollNumber will be sorted on ascending order.

```csharp
		List<string> sortedStandard = new List<string>() {"Second", "First", "Third"};
		List<string> sortedSection = new List<string>() {"B", "A"};
```

Now, we have created everything required to proceed ahead. Let's sort our List based on our requirement mentioned in the form of sorted lists.

```csharp
	List<Student> sortedStudents = students.
			OrderBy(x => sortedStandard.IndexOf(x.standard)).
			ThenBy(x => sortedSection.IndexOf(x.section)).
			ThenBy(x => x.rollNumber).ToList();
```

That's all!. Isn't it easier? Instead of writing the chain of looping statements and conditionals, we achieved the required result within a single statement using a Linq. 

Here is the output of our program.

```
{
   name        : Harry
   rollNumber  : 1
   section     : B
   standard    : Second
   },
   {
   name        : Penny
   rollNumber  : 4
   section     : B
   standard    : Second
   },
   {
   name        : Smith
   rollNumber  : 5
   section     : B
   standard    : Second
   },
   {
   name        : Elon
   rollNumber  : 1
   section     : A
   standard    : Second
   },
   {
   name        : Selena
   rollNumber  : 3
   section     : B
   standard    : First
   },
   {
   name        : Tylor
   rollNumber  : 1
   section     : A
   standard    : First
   },
   {
   name        : Diana
   rollNumber  : 1
   section     : A
   standard    : First
   },
   {
   name        : Jack
   rollNumber  : 8
   section     : A
   standard    : Third
   },
   {
   name        : Bob
   rollNumber  : 10
   section     : A
   standard    : Third
   }   
```

## How did it work?

Let's drill down our LINQ expression and understand how it worked.

sortedStandard.IndexOf(x.standard) searches the specified property of list and returns the zero-based index of the first occurrence within the sortedStandard list. For example:

"Third" => 2

"Second" => 0

The order by clause sorts the values in ascending order of the indexes.

Once the list is sorted by the standard, ThenBy clause performs a secondary sort in ascending order on that list in a similar fashion. Finally, the list thus obtained is sorted in ascending order based on the rollNumber.

Hope it was helpful. Keep coding :)