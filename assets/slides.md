### Hack for Social Impact Summit
# Ruby on Rails Workshop

----

# Development Environment
* ide.goorm.io
  * All on the web!
  * Installation takes time
* Local development (preferred)
  * Installation guide
  * Docker
    * https://github.com/FranCogMents/dockerLabs

Note:
* [Cloud IDE](https://ide.goorm.io/)
    * Provides you a integrated development environment on the cloud -- supports Ruby on Rails!
* [Docker](https://github.com/FranCogMents/dockerLabs)
    * Experimental Repository -- allows you to run Rails without having to install the framework directly on your machine

---

# Backside of Web
### Everything is requests!

Note:
caveat the division of backend and frontend disappearing

----

# The Power of Requests

----

# Anatomy of a Request

The important parts of a request: 

**URL**: The address you want to send the request to
<!-- .element: class="fragment" -->

**Request Method**: The type of request you want to send
<!-- .element: class="fragment" -->

**Body**: Additional, optional, secure data we want to send with a request
<!-- .element: class="fragment" -->

----

# What is in a url?
![](https://i.imgur.com/Ewd2GlO.png)

----

# Query Parameters

- Request parameters are sent through the url itself!
- Sending as params `{"key1":"value1", "name":"Frederick Kim"}` to https://www.facebook.com/user
- Turns into: https://www.facebook.com/user?key1=value1&name=Frederick%20Kim
    - `key1=value1&name=Frederick%20Kim` is the added part

----

# Anatomy of a Response

**Status Code:** A code to tell you whether the request succeeded or failed and why
<!-- .element: class="fragment" -->

**Body:** The data we asked for in the request (text, html, files)
<!-- .element: class="fragment" -->

----

# We are building a web server!

- Our job is to respond to these requests
<!-- .element: class="fragment" -->

- Rails hides the complexity for us
<!-- .element: class="fragment" -->

- How do we access request params, headers, and body?
<!-- .element: class="fragment" -->

---

# Ingredients of the Backend

----

# MVC
<div>
<ul>
  <li>Model</li>
  <ul>
    <li> Structure of data</li>
  </ul>
  <li>View</li>
  <ul>
    <li>User interface</li>
  </ul>
  <li>Controller</li>
  <ul>
    <li>Request handler</li>
  </ul>
  <li>+ Routes</li>
  <ul>
    <li>Endpoint</li>
  </ul>
</ul>
</div>

----

![](https://i.imgur.com/4Qkq9W0.png)

---

# Routes

----

# Routes
* Act as an endpoint for both the browser and the server
* Rails router recognizes URLs and dispatches them to a controller's action

----

### Throwback to URLs
`config/routes.rb`
```ruby
# Two versions of the same get route
get '/home/index', action: :index, controller: 'home'
get '/home/index', to: 'home#index'

# Two versions of the same post route
post '/home/update', action: :update, controller: 'home'
post '/home/update', to: 'home#update'
```

---

# Controller

----

# Controller
* Controller's role is to take the request from the router and produce the appropriate result 

---

### Controller 

```ruby
class WorkshopsController < ApplicationController
  def index
    @Workshops = Workshop.all
  end
end
```

---

# View

----

# View
* How rails presents a response to the browser

----

# View
```ruby
<h1>Workshops</h1>
<% @workshops.each do |workshop| %>
  <h2><%= workshop.name %></h2>
<% end %>
```
* Embedded Ruby is a templating system that embeds Ruby into a text document 

---

# Model

----

# Model
* Rails allows you to specify structured database records
* These records can have relations to other records

----

# Database
A way to structure data

**Cities**

| ID | Name | Temperature | Description |
| -------- | -------- | -------- | ---- |
| 1     | Berkeley     | 50.4°     | partly cloudy |
| 2 | Los Angeles | 70.6° | clear |
| 3 | New York | 76° | sunny |

----

## How do you interact with a database?

or... HOW DO YOU INTERACT WITH A DATABASE;

```sql
SELECT * FROM STATION 
WHERE 50 < (SELECT AVG(TEMP_F) FROM STATS 
WHERE STATION.ID = STATS.ID);
```

----

## Rails does it for you

Just getting the first record is easier!

```ruby
City.first
```

generates

```sql
SELECT * FROM cities ORDER BY cities.id ASC LIMIT 1
```

----

## Levels of a database
![](https://i.imgur.com/EG7sf6s.png)

----

# Relational Modeling

----

## Modeling

- Rails allows you to specify structured database records
- These records can have _relations_ to other records

----

## Relations
**One to one**: A `User` might have one `Profile` (with more information)
<!-- .element: class="fragment" -->
**One to many**: A `Customer` might have many `Purchase`s.
<!-- .element: class="fragment" -->
**Many to many**: A `Friend` might have many `Friend`s, and vice versa.
<!-- .element: class="fragment" -->

----

<div>
  <img src="https://i.imgur.com/1ST6tAO.png" height="650" />
</div>

----

# Once again a high-level view
![](https://i.imgur.com/4Qkq9W0.png)

---

# Why Rails?

----

* Fast setup of scalable application
<!-- .element: class="fragment" -->
* Very fast development
<!-- .element: class="fragment" -->
* Opinionated & Omakase
  * Pros and Cons
<!-- .element: class="fragment" -->

----

# Structure of a Rails project


----

# Rails Magic
### How does Rails know????
* We don't know (or at least don't need to know)
* Strict standards = highly opinionated
  * Same name between controllers, routes, views to connect
  * Strict file structure
  * Controllers should be plural
  * Models should be singular

---

# Quick Intro to Ruby
Key Differences
* Everything is an object
* No typedef
* Variables
* Symbols

----

## Objects everywhere
```ruby=
{ 
    1 => Integer, 
    ‘String’ => String, 
    :symbol => Symbol, 
    [] => Array, 
    {} => Hash, 
    nil => NilClass 
}
```

----

## No typedef
* Just like Python
```ruby
hello = 'hello'
two = 2
arr = [10, 'Social', true]
```

----

## Variables
* @ for instance variables
* $ for global variables
* nothing for local variables

----

## Symbols
Not a string nor a variable
<!-- .element: class="fragment" -->
They are unique identifiers
<!-- .element: class="fragment" -->
```ruby
{ :one => "eins", :two => "zwei", :three => "drei" }
# JSON-like
{ one: "eins", two: "zwei", three: "drei" }
```
<!-- .element: class="fragment" -->
* Typically used for keys in hashes
<!-- .element: class="fragment" -->

---

# Google is your friend!
### *(except with your data)*

---

# Demo
## MB4H4SISW

----

# Message Board for H4SIS Workshops
* Features
    * What should it be able to do?
* Models
    * What is our schema?

----

# Models
<table style="font-size: 0.8em">
  <thead>
    <tr>
      <th></th>
      <th>Fields</th>
      <th>Associations</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Workshops</td>
      <td>
        <div class="fragment" data-fragment-index="1">name: string</div>
      </td>
      <td>
        <code class="fragment" data-fragment-index="4">has_many :posts</code>
      </td>
    </tr>
    <tr>
      <td>Posts</td>
      <td class="fragment" data-fragment-index="2">
        <div>title: string</div>
        <div>body: text</div>
      </td>
      <td>
        <code class="fragment" data-fragment-index="5">belongs_to :workshop</code><br>
        <code class="fragment" data-fragment-index="7">belongs_to :hacker</code>
      </td>
    </tr>
    <tr>
      <td>Hackers</td>
      <td class="fragment" data-fragment-index="3">
        <div>email: string</div>
        <div>password: string</div>
        <div>first name: string</div>
        <div>last name: string</div>
      </td>
      <td>
        <code class="fragment" data-fragment-index="6">has_many :posts</code>
      </td>
    </tr>
  </tbody>
</table>


----

# Quick Aside: Gems
* Packages/Libraries
* Make development quicker and easier
* Use Devise for authentication

----

# Now it's your turn!
## We want comments!

---

# Thanks for coming!
