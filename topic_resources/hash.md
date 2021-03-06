# Hashes

Hash's in Ruby are used often to represent an object instead of or before an actual class object.
This often happens when we get some type of input that can be parsed into sane parts. This could come in many different formats such as JSON, XML, YAML, or CSV.
For example if we have a CSV:

| name              | email                                   |
|:------------------ |:----------------------------------------|
| Bookis Smuin   | bookis@adadevelopersacademy.org |
| Karen Hambro   | karen.hambro@adadevelopersacademy.org |

Each line of this could be represented as a hash, using the headers as the keys:

```ruby
{name: "Bookis Smuin", email: "bookis@adadevelopersacademy.org"}
```
```ruby
{name: "Karen Hambro", email: "karen.hambro@adadevelopersacademy.org"}
```

Further we could groups these in an Array:
```ruby
[{name: "Bookis Smuin", email: "bookis@adadevelopersacademy.org"},
{name: "Karen Hambro", email: "karen.hambro@adadevelopersacademy.org"}]
```

A `Hash` key can have any object as it's value, even another hash.

```ruby
{bookis:
  {
    last_name: "Smuin",
    first_name: "Bookis",
    address: {
      street: "123 fake st",
      city: "Seattle",
      state: "WA"
    },
    children: [{
      name: "Isaac",

    }],
    pets: [{
      type: "cat",
      name: "Urchin Jr."
    }]
  }
}
```
Using Hash to initiate objects
---------
A Hash is a great way to pass in arguments to `initialize`, first let's look at a use case for this.
```ruby
class Address
  def initialize(first_name, last_name, street_one, street_two, city, state, country, postal_code)
    @first_name  = first_name
    @last_name   = last_name
    @street_one  = street_one
    @street_two  = street_two
    @city        = city
    @state       = state
    @country     = country
    @postal_code = postal_code
  end
end
Address.new("Bookis", "Smuin", "123 fake st", "seattle", "WA", "US", 98102)
```

What is the problem (or at least obnoxious) there? What if you don't have a `street_two` attribute?

Let's try again using a hash
```ruby
class Address
  def initialize(address_hash)
    @first_name  = address_hash[:first_name]
    @last_name   = address_hash[:last_name]
    @street_one  = address_hash[:street_one]
    @street_two  = address_hash[:street_two]
    @city        = address_hash[:city]
    @state       = address_hash[:state]
    @country     = address_hash[:country]
    @postal_code = address_hash[:postal_code]
  end
end

Address.new(first_name: "Bookis")

```
Example
--------
```ruby
books = {
  top_time_travel: [
    {
      title: "The Time Machine",
      author: "H. G. Wells",
      category: "Fiction",
      rating: (4 + 4.5 + 3 + 5 + 4.5) / 5,
      sales: {1895 => 3_000_000},
      plot: {
        year: 802701,
        species: ["Morlocks", "Eloi"]
      }
    },
    {
      title: "A Connecticut Yankee in King Arthur's Court",
      author: "Mark Twain",
      category: "Fiction",
      rating: (4.5 + 4.5 + 2 + 5 + 4.5 + 4) / 6,
      sales: {1889 => 2_100_000},
      plot: {
        year: 528,
        species: ["Human"]
      }
    }
  ]
}
```
