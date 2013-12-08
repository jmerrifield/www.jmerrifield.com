---
title: Readable String Concatenation
date: 2010-02-17 12:00
template: article.jade
---

When interviewing for .NET jobs, invariably something comes up along the lines of: "If you had to join a number of strings together, how would you do it?".  Sadly, the desired answer is usually a combination of [micro-optimisation][1], and poor awareness of the [relative performance][2] of various string concatenation methods - a textbook [StringBuilder][4] implementation.

Regardless of which method you use, you can't escape the fact that most string concatenation code is ugly as hell, let's look at a few ways you could create a comma separated list of customers names, each one surrounded with quotes:

```cs
// Set up our test data
const string separator = ", ";
const string quote = "'";
var customers = new[] { "Chuck Norris", "Bruce Lee", "Bear Grylls", "Ray Mears" }
  .Select(x => new Customer { Name = x });
```

```cs
// Standard string concatenation
string result = string.Empty;
foreach (var customer in customers)
{
  result += quote + customer.Name + quote;
  if (customer != customers.Last())
  {
    result += separator;
  }
}

return result;
```

```cs
// Textbook StringBuilder usage
var builder = new StringBuilder();
foreach (var customer in customers)
{
  builder.Append(quote);
  builder.Append(customer.Name);
  builder.Append(quote);
  if (customer != customers.Last())
  {
    builder.Append(separator);
  }
}

return builder.ToString();
```

```cs
// It gets a little better with string.join
var names = customers.Select(x => quote + x.Name + quote);
var nameArray = names.ToArray();

return string.Join(separator, nameArray);
```

It's surprising how this fairly simple task turns into such a lot of code, none of it particularly intention-revealing.  The most unfriendly one appears to be the StringBuilder implementation.  As a side note, I expect most people wouldn't bother defining constants for 'quote' and 'separator', since they're unlikely to change, and only one character long anyway, but in this case having an obvious and explicit name for each one makes it clearer at a first glance to see the intention behind the code (see [ScreechinglyObviousCode][3]).

With a few very simple extension methods, which look like they would come in handy all over, we can reduce this task to the amount of code that it seems like it should take - a screamingly obvious one-liner.

```cs
public static string ConcatStrings(this IEnumerable<string> source, string separator)
{
  if (source == null) throw new ArgumentNullException("source");
  return string.Join(separator, source.ToArray());
}

public static string Wrap(this string source, string wrapper)
{
  return wrapper + source + wrapper;
}
```

Now we can use this:

```cs
return customers.Select(x => x.Name.Wrap(quote)).ConcatStrings(separator);
```

It's always worth adding a few simple utility methods to help make your core business logic code more readable and intention-revealing.  With extension methods our utility functions can be easily discoverable and obviously named (no more big-bag-o-crap static utility classes with hundreds of badly-named, unrelated functions!)

[1]: http://www.codinghorror.com/blog/2009/01/the-sad-tragedy-of-micro-optimization-theater.html
[2]: http://www.codeproject.com/KB/cs/StringBuilder_vs_String.aspx
[3]: http://c2.com/cgi/wiki?ScreechinglyObviousCode
[4]: http://msdn.microsoft.com/en-us/library/system.text.stringbuilder(v=vs.80).aspx