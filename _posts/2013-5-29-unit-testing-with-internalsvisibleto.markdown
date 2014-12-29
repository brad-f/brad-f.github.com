---
layout: post
title: "Unit Testing with InternalsVisibleTo"
date: 2013-5-29
categories: csharp testing
---

When developing a library, its useful to restrict access to Utility/Helper classes with the internal access modifier. From the C# [reference][csharp-ref]:

> A common use of internal access is in component-based development because it enables a group of components to cooperate in a private manner without being exposed to the rest of the application code. For example, a framework for building graphical user interfaces could provide Control and Form classes that cooperate using members with internal access. Since these members are internal, they are not exposed to code that is using the framework.

Well defined boundaries always improve maintainability. This is critical when your assemblies are published via NuGet and you want to minimize breaking changes as your code evolves.  Reducing the amount of code that can be accessed by the consumer makes the assembly easier to maintain.

However, when unit testing, this type of encapsulation can work against you. How can you test the internal methods from a test assembly when the methods are inaccessible? Luckily, the .Net framework solves this problem with the InternalsVisibleTo attribute. InternalsVisibleTo is an assembly level attribute that allows the developer to create Friend Assemblies, which have access to internal types and methods.  For example, given these two assemblies:

* Component.One  has some some internal types/methods
* Component.One.Test  a unit test assembly.

You can make Component.One.Test a Friend Assembly of Component.One by adding this line to Component.Ones AssemblyInfo.cs:

{% highlight C# %}
  [assembly: InternalsVisibleTo("Component.One.Test")]
{% endhighlight %}

Like most things, InternalsVisibleTo can be abused. I find its very useful for unit testing, but would hesitate to use it for anything else. Lastly, there are a few caveats when assemblies are strong-named, so I recommend reading the [documentation][doc].

[csharp-ref]: http://msdn.microsoft.com/en-us/library/7c5ka91b(v=vs.80).aspx
[doc]: http://msdn.microsoft.com/en-us/library/system.runtime.compilerservices.internalsvisibletoattribute.aspx
