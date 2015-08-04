# CoffeeScript Style Guide

CoffeeScript Style Guide to maintain readable code, that looks like it was written by one person, even if a whole team was working on it.
Highly inspired by [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript/tree/8d2a83385795b8a3763890a344f9592e36ed9407/es5)

## Table of contents
1. [CoffeeScript syntax](#coffeescript-syntax)
2. [Tabs](#tabs)
3. [Whitespace](#whitespace)
4. [Semicolons](#semicolons)
5. [Commas](#commas)
6. [Naming conventions](#naming-conventions)
7. [Variables](#variables)
8. [Objects](#objects)
9. [Accessors](#accessors)
10. [Arrays](#arrays)
11. [Strings](#strings)
12. [Events](#events)
13. [Functions](#functions)
14. [Iterators](#iterators)
15. [Type casting](#type-casting)
16. [Comparison Operators & Equality](#comparison-operators--equality)
17. [Comments](#comments)
18. [jQuery](#jquery)

### CoffeeScript syntax
- [1.1](#1.1) Do not use braces `(` for function calls with parameters.
```coffeescript
  createPerson = (name) ->
    console.log 'Created!'
  createPerson 'John Doe'
  
  showMessage = ->
    console.log 'This is a message'
  showMessage()
```
- [1.2](#1.2) Do not use curly braces `{` for declaring objects.
```coffeescript
  person =
    name: 'John Doe'
```
- [1.3](#1.3) Use curly braces `{` for declaring empty objects.
```coffeescript
  emptyObject = {}
```
- [1.4](#1.4) Use the `class` keyword to create classes, instead of working directly with `prototype`.
```coffeescript
  class Person
    constructor: ->
      console.log 'Person constructed!'
```
- [1.5](#1.5) Do not use braces `(` for empty parameter lists.
```coffeescript
  emptyParameterListFunction = ->
    console.log 'I have no parameters and no braces'
```

### Tabs
- [2.1](#2.1) Use soft spaces instead of tabs.
- [2.2](#2.2) Use an intendation of 2 spaces.

**[⬆ back to top](#table-of-contents)**


### Whitespace
- [3.1](#3.1) Place one space after the trailing brace.
```coffeescript
  addition = (a, b) ->
    console.log a + b
```

- [3.2](#3.2) Set off operators with spaces.
```coffeescript
  x = 1 + 2
```

- [3.3](#3.3) Use indentation when making long method chains. Use a leading dot, which emphasizes that the line is a method call, not a new statement.
```coffeescript
  $('.items').addClass '.additional-class'
  .attr 'width', '110'
  .attr 'height', '150'
```

**[⬆ back to top](#table-of-contents)**


### Semicolons
- [4.1](#4.1) Don't use them.
```coffeescript
  age = 21 # Don't use semicolons
```

**[⬆ back to top](#table-of-contents)**


### Commas
- [5.1](#5.1) Don't use trailing commas.
```coffeescript
  numbers = [
      1
      2
      3
  ]
  mapping =
    a: 1
    b: 2
    c: 3
```

**[⬆ back to top](#table-of-contents)**


### Naming conventions
- [6.1](#6.1) Use camelCase when naming objects, functions, variables, and instances.
```coffeescript
  firstName = 'John'
  myObject = {}
  testFunction = ->
    return
```

- [6.2](#6.2) Use SNAKE_CASE and uppercase for constants.
```coffeescript
  API_URL = '/api'
```

- [6.3](#6.3) Use PascalCase when naming classes.
```coffeescript
  self = undefined
  class Person
    name: 'John Doe'
    
    constructor: (options) ->
      self = @
      self.name = options.name
```

- [6.4](#6.4) Use a leading underscore `_` when naming private properties.
```coffeescript
  @_firstName = 'John'
```

- [6.5](#6.5) Don't use reserved words.
```coffeescript
  # bad
  default = 42
  # good
  defaultNumber = 42
```

**[⬆ back to top](#table-of-contents)**


### Variables
- [7.1](#7.1) Because CoffeeScript knows no `var` keyword, variables are always declared without it. If you want to declare global variables, use the `window` object.
```coffeescript
  name = 'John Doe'
  window.env = 'local'
```

**[⬆ back to top](#table-of-contents)**


### Objects
- [8.1](#8.1) Use the literal syntax for object creation.
```coffeescript
  person =
      name: 'John Doe'
```

- [8.2](#8.2) Methods can return this to help with method chaining.
```coffeescript
  class Person
    walk: (meters) ->
      console.log 'I walked ${meters}m'
      return @
    jump: ->
      console.log 'I jumped very high'
      return @

  person = new Person()
  person.walk()
  .jump()
```

- [8.3](#8.3) Use dot notation when accessing properties.
```coffeescript
  person =
    name: 'John Doe'
  name = person.name
```

- [8.4](#8.4) Use subscript notation `[]` when accessing properties with a variable.
```coffeescript
  person =
    name: 'John Doe'
  property = 'name'
  name = person[property]
```

- [8.5](#8.5) Use `@` instead of `this`.
```coffeescript
  self = undefined
  class Person
    name: ''
    
    constructor: (options) ->
      self = @
```

- [8.5](#8.5) Use a variable called `self` to refer to the `this` context of objects.
```coffeescript
  self = undefined
  class Person
    name: ''
    
    constructor: (options) ->
      self = @
      self.name = options.name
```

**[⬆ back to top](#table-of-contents)**


### Accessors
- [9.1](#9.1) Accessor functions for properties are not required.

- [9.2](#9.2) If you do make accessor functions use `getVal()` and `setVal('hello')`.
```coffeescript
  person.setAge 21
  age = person.getAge()
```

- [9.3](#9.3) If the property is a `boolean`, use `isVal()` or `hasVal()`.
```coffeescript
  if person.hasCoffee()
    console.log 'I am alive'
  if person.isAlive()
    console.log 'I have coffee'
```

- [9.4](#9.4) It's okay to create `get()` and `set()` functions, but be consistent.
```coffeescript
  self = undefined
  class Person
    name: ''
    
    constructor: (options) ->
      self = @
      self.set 'name', options.name
      
    set: (key, val) ->
      self[key] = val
      
    get: (key) ->
      return self[key]
```

**[⬆ back to top](#table-of-contents)**


### Arrays
- [10.1](#10.1) Use the literal syntax for array creation.
```coffeescript
  persons = []
```

- [10.2](#10.2) Use Array#push instead of direct assignment to add items to an array.
```coffeescript
  persons = []
  person =
    name: 'John Doe'
  persons.push person
```

- [10.3](#10.3) Use `slice` to copy arrays.
```coffeescript
  numbers = [4, 2]
  numbersCopy = numbers.slice()
```

**[⬆ back to top](#table-of-contents)**


### Strings
- [11.1](#11.1) Use single quotes `''` for strings.
```coffeescript
  name = 'John Doe'
```

- [11.2](#11.2) Strings longer than 100 characters should be written across multiple lines using string concatenation.
```coffeescript
  description = 'I'm a very long text and need to be written across multiple lines using string ' + 
    'concatenation.'
```

- [11.3](#11.3) **Note**: If overused, long strings with concatenation could impact performance. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40). 

- [11.4](#11.4) When programmatically building up strings, use template strings instead of concatenation.
```coffeescript
  person =
      name: 'John Doe',
      walk: (meters) ->
        return '${this.name} walked ${meters}m.'    
```


### Functions
- [12.1](#12.1) Never declare a function in a non-function block (if, while, etc). Assign the function to a variable instead. Browsers will allow you to do it, but they all interpret it differently, which is bad news bears.
```coffeescript
  # Don't do this!
  if isTrue
      createPerson = ->
      return
```

**[⬆ back to top](#table-of-contents)**


### Events
- [13.1](#13.1) When attaching data payloads to events (whether DOM events or something more proprietary like Backbone events), pass a hash instead of a raw value. This allows a subsequent contributor to add more data to the event payload without finding and updating every handler for the event.
```coffeescript
  $(this).trigger 'productBought',
    productId: 42
  $(this).on 'productBought', (e, data) ->
    productId = data.productId
```

**[⬆ back to top](#table-of-contents)**


### Iterators
- [14](#14.1) Don't use iterators. Prefer JavaScript's higher-order functions like map() and reduce() instead of loops like for-of.
```coffeescript
  numbers = [4, 2]
  numbers.forEach (num) ->
    console.log num
```

**[⬆ back to top](#table-of-contents)**


### Type Casting
- [15.1](#15.1) Use `String` for strings.
```coffeescript
  stringValue = String 42
```

- [15.2](#15.2) Use `parseInt` for Numbers and always with a radix for type casting.
```coffeescript
  intValue = parseInt '42', 11
```

- [15.3](#15.3) Use `Boolean` for booleans.
```coffeescript
  isTrue = Boolean 0
```

**[⬆ back to top](#table-of-contents)**


### Comparison Operators & Equality
- [16.1](#16.1) Use `is` and `isnt` over `===` and `!==`.

- [16.2](#16.2) **Note:** Conditional statements such as the if statement evaluate their expression using coercion with the ToBoolean abstract method and always follow these simple rules:
    + Objects evaluate to true
    + Undefined evaluates to false
    + Null evaluates to false
    + Booleans evaluate to the value of the boolean
    + Numbers evaluate to false if +0, -0, or NaN, otherwise true
    + Strings evaluate to false if an empty string '', otherwise true
    ```coffeescript
      if [0]
        # true
        # An array is an object, objects evaluate to true
        return
    ```
    
- [16.3](#16.3) Use shortcuts.

- [16.4](#16.4) **Note:** For more information see [Truth Equality](https://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) and JavaScript by Angus Croll.

**[⬆ back to top](#table-of-contents)**


### Comments
- [17.1](#17.1) Use ###* ... ### for multi-line comments. Include a description, specify types and values for all parameters and return values.
```coffeescript
  ###*
     * Create a new person.
     *
     * @since 1.0.0
     * @param {string} name
     * @return {Person}
   ###
   createPerson = (name) ->
      return new Person
        name: name
```

- [17.2](#17.2) **Note:** For more information see [JSDoc](http://usejsdoc.org/).

- [17.3](#17.3) Use `# FIXME:` to annotate problems.
```coffeescript
  # FIXME: Something is wrong here, please fix it
```

- [17.4](#17.4) Use `# TODO:` to annotate solutions to problems.
```coffeescript
  # TODO: Write more code!
```

**[⬆ back to top](#table-of-contents)**


### jQuery
- [18.1](#18.1) Cache jQuery lookups.
```coffeescript
  setSidebar = ->
    sidebar = $('.sidebar')
    sidebar.hide()
    sidebar.show()
```

**[⬆ back to top](#table-of-contents)**