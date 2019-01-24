# Ruby Fundamental Classes

Let's get acquainted with some of the basic Ruby classes. Try the following in `rails console`.

## Fixnum

`Fixnum` is Ruby's name for integers. You can prove it by doing

```ruby
7.class
```

In fact, you can always call `.class` on *any* object, ever, at any time, to ask it what class it is. You can also call `.methods` to find out what all it can do, but the resulting list is pretty hard to look at so I usually use some other resources instead, which I'll direct you to later.

Try:

```ruby
7.odd?     # The question mark is nothing special,
           #   just another letter in the method name
7.days.ago
rand(10)   # Produces a random integer between 0 and 9
7.to_s     # Convert yourself to a string; probably so
           #   you can be added to other strings 
```

Why wouldn't `"7".even?` work? Take a guess before you try it, and see if your guess matches up with what the error message says.

There are also the usual calculator-like things; try each of the following:

```ruby
7 * 6
21 + 21
45 - 3
3**2       # Heads up: you might have been expecting the syntax for
           #   "three raised to the power of 2" to be 3^2
10 / 3
```

Whoa, what's up with that last one? Well, it turns out that when you divide an integer by an integer in Ruby, it returns an integer (without the remainder). Like in grade school division. (You can also get the remainder with `10 % 3`; `%` is called the "modulus" operator.)

If you want the decimal version, then at least one of the two operands needs to be a...

## Float

Ruby calls decimal numbers `Float`s. Try

```ruby
n = 3.141592
n.round(2)

10.0 / 3
10 / 3.0
rand       # rand without any arguments produces a random
           #   number between 0 and 1; useful for probabilities
```

I won't say too much more about `Float`s for now, since they are mostly the same as `Fixnum`s. Use them as needed, but I try to default to integers.

## String

We've already met the `String` class a few times, but here are some handy methods to try:

```ruby
a = "Hello"
b = "World!"
a + b        # You can add strings
a + " " + b
a * 3        # Yup.
3 * a        # Nope.
a.upcase
a.downcase
a.swapcase
a.reverse
a.length
b.chomp("!")
b.chomp(".") # What is .chomp() doing?
a.gsub("ll", "✌️") 
             # What is .gsub() doing?
             #   Experiment with other strings and arguments.
```

Sometimes you have a string that contains a number, usually input from a user, and want to do math on it:

```ruby
i = "10"
i / 3      # Uh oh.
```

You can use `.to_i` to convert the string to an integer, or `.to_f` to convert it to a decimal (a "float"):

```ruby
i = "7"
i.to_i / 3
i.to_f / 3
```

What would you expect Ruby to do with the following expressions? Return a value? Throw an error?

```ruby
"7 apples".to_f
"apples".to_f
```

Give them a try!

---

Here are some other, more realistic examples:

```ruby
u = "  a messy, input   string123!@$    \n"
                  # The \n at the end represents a newline

u.chomp           # .chomp with no arguments will default to "\n"

u.strip           # .strip removes all leading and trailing whitespace

u.gsub(/\s+/, "") # This is an advanced technique that removes all whitespace

u.gsub(/[^a-z0-9\s]/i, "")
                  # This is an advanced technique that removes
                  #   everything except alphanumerics and whitespace

u.capitalize      # Oops. Why?

u = u.gsub(/[^a-z0-9\s]/i, "").strip
                  # Let's save a sanitized version.

u.capitalize
u.titlecase
u.split           # This produces an Array, which we discuss below.
u.split.count     # Arrays are lists, and can be counted.

"lo".in?("hello")
"".present?
"".blank?
"hi".present?
"hi".blank?
```

We spend a lot of time composing strings of output for our users, so let's see a few more examples. Try this:

```ruby
message = "Your lucky number for today is " + rand(100) + "."
```

You'll see that Ruby gets confused, because we are trying to add an integer to a string and it doesn't feel comfortable with that.

The solution is to tell the integer to convert itself to a string first:

```ruby
message = "Your lucky number for today is " + rand(100).to_s + "."
```

The above technique for composing strings, adding them together with `+`, is called **string concatenation**.

There's another technique for composing strings that I personally find a bit easier; it's called **string interpolation**. It goes like this:

```ruby
message = "Your lucky number for today is #{rand(100)}."
```

Basically, inside the string, you place `#{}` where you eventually want your value to go. Inside the curly braces, you can write any Ruby expression without worrying about whether it is a string or not. The expression will be evaluated, converted to a string, and added to the string right in that spot. You can interpolate as many expressions as you want into a single string. Pretty neat!

If you find interpolation confusing, feel free to just use concatenation.

## Date

Dates are very tricky to work with, especially when you take timezones into account, but Ruby makes it as easy as possible. Try the following:

```
t = Date.today
t.wday
t.friday?
```

## Arrays

Finally, we have a very important class: `Array`. Most of what we do as web developers is manage *lists of things*. Lists of photos, likes, followers, reviews, listings, messages, whatever.

The first structure we're going to learn to help us manage lists is `Array`. Here's how they work:

```ruby
a = [8, 3, 1, 19, 23, 3]
```

 - The way we create `String`s by wrapping the string of characters in double-quotes, we create `Array`s by wrapping the list of elements in square brackets.
 - Seperate elements in the list with commas.

Now that we've created our array, what can we do with it? Here are some handy methods to try:

```ruby
a.count        # Counts all elements in the list.
a.count(3)     # Counts the occurrences of the argument.

a.reverse
a.sort
a.sort.reverse

a.shuffle
a.sample

a.min
a.max
a.sum

a.first
a.last
a.second
a.at(3)           # Accesses the 4th element! Surprising.
a.at(0)           # Arrays start their numbering at 0.
a.at(-1)
a[3]              # This is a shorthand syntax for .at(3).
                  #   I prefer a.at() but a[] is more common.

a.push(42)
a.count
a.last
```

## To Learn More

That's a fun selection of some common methods, but obviously there are a lot more. To learn more, usually my MO is: start building something, run into a situation where I need a new tool, like: "How do I find what spot in an array a particular element is at?"

Then, you should, in order:

 - Post a question on Piazza. You are brand new to programming and the answers that you will find on the internet will oftentimes be advanced or just flat out wrong, and you won't yet be able to tell the difference easily. So for now, lean on us and each other.
 - Check the Ruby Docs for whichever class you are wondering about. In this case, the [Array docs](https://ruby-doc.org/core-2.2.0/Array.html). Scan the method list on the left until you see something that looks kinda right, and then check out the examples. (In this case, [#index](https://ruby-doc.org/core-2.2.0/Array.html#method-i-index) sounds about right.)
 - Google it and hope to find a helpful blog post or Stack Overflow answer.
 - Trial and error! The life of a developer.

## Next Up

Alright! It's been fun playing around with Ruby in the `rails console`, but how would we actually builds some real, [permanent programs](permanent-programs.md) that we can share with our friends? That's what we'll see next.
