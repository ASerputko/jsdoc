# The Basics of JSDoc

JSDoc is all about documenting *entities* (functions, methods, constructors, etc.). That is achieved via comments that precede the entities and start with `/**`.

#### SYNTAX
Let’s review the comment shown at the beginning:
```javascript
/**
 * Repeat <tt>str</tt> several times.
 * @param {string} str The string to repeat.
 * @param {number} [times=1] How many times to repeat the string.
 * @returns {string}
 */
```

This demonstrates some of the JSDoc syntax, which consists of the following pieces:
##### *JSDoc comment*
This is a JavaScript block comment whose first character is an asterisk. This creates the illusion that the token `/**` starts such a comment.
##### *Tags*
You structure comments by starting lines with *tags*, keywords that are prefixed with an @ symbol. `@param` is an example in the preceding code.
##### *HTML*
You can freely use HTML in JSDoc comments. For example, `<tt>` displays a word in a monospaced font.
##### *Type annotations*
You can document the type of an entity via a type name in braces. Variations include:
- Single type: @param {string} name
- Multiple types: @param {string|number} idCode
- Arrays of a type: @param {string[]} names

##### *Namepaths*
Inside JSDoc comments, so-called *namepaths* are used to refer to entities. The syntax of such paths is as follows:
```javascript
myFunction
MyClass
MyClass.staticMember
MyClass#instanceMember
```
*Classes* are usually (implemented by) constructors. Static members are, for example, properties of constructors. JSDoc has a broad definition of *instance member*. It means everything that can be accessed via an instance. Therefore, instance members include instance properties and prototype properties.

#### NAMING TYPES
The types of entities are either primitive types or classes. The names of the former always start with lowercase letters; the names of the latter always start with uppercase letters. In other words, the type names of primitives are *boolean*, *number*, and *string*, just like the results returned by the typeof operator. That way, you cannot confuse strings (primitives) with instances of the constructor *String* (objects).

# Basic Tags

Following are the basic metadata tags:

`@fileOverview` description

Marks a JSDoc comment that describes the whole file. For example:
```javascript
/**
 * @fileOverview Various tool functions.
 * @author <a href="mailto:jd@example.com">John Doe</a>
 * @version 3.1.2
 */
```
`@author`

Refers to who has written the entity being documented.

`@deprecated`

Indicates that the entity is not supported anymore. It is a good practice to document what to use instead.

`@example`

Contains a code example illustrating how the given entity should be used:
```javascript
/**
 * @example
 * var str = 'abc';
 * console.log(repeat(str, 3)); // abcabcabc
 */
```

Basic tags for linking are as follows:

`@see`

Points to a related resource:
```javascript
/**
 * @see MyConstructor#myMethod
 * @see The <a href="http://example.com">Example Project</a>.
 */
```
`{@link ...}`

Works like @see, but can be used inside other tags.

`@requires resourceDescription`

Indicates a resource that the documented entity needs. The resource description is either a namepath or a natural language description.

Versioning tags include the following:

`@version versionNumber`

Indicates the version of the documented entity. For example:
```javascript
@version 10.3.1
```
`@since versionNumber`

Indicates since which version the documented entity has been available. For example:
```javascript
@since 10.2.0
```

# Documenting Functions and Methods

For functions and methods, you can document parameters, return values, and exceptions they may throw:

`@param {paramType} paramName description`

Describes the parameter whose name is paramName. Type and description are optional. Here are some examples:
```javascript
@param str The string to repeat.
@param {string} str
@param {string} str The string to repeat.
```
Advanced features:

- Optional parameter:
```javascript
@param {number} [times] The number of times is optional.
```
- Optional parameter with default value:
```javascript
@param {number} [times=1] The number of times is optional.
```

`@returns {returnType} description`

Describes the return value of the function or method. Either type or description can be omitted.

`@throws {exceptionType} description`

Describes an exception that might be thrown during the execution of the function or method. Either type or description can be omitted.

# Inline Type Information (“Inline Doc Comments”)

There are two ways of providing type information for parameters and return values. First, you can add type annotations to @param and @returns:
```javascript
/**
 * @param {String} name
 * @returns {Object}
 */
function getPerson(name) {
}
```
Second, you can inline the type information:
```javascript
function getPerson(/**String*/ name) /**Object*/ {
}
```

# Documenting Variables, Parameters, and Instance Properties
The following tags are used for documenting variables, parameters, and instance properties:

`@type {typeName}`

What type does the documented variable have? For example:
```javascript
/** @type {number} */
var carCounter = 0;
```
This tag can also be used to document the return type of functions, but @returns is preferable in this case.

`@constant`

A flag that indicates that the documented variable has a constant value.
```javascript
/** @constant */
var FORD = 'Ford';
```
`@property {propType} propKey description`

Document an instance property in the constructor comment. For example:
```javascript
/**
 * @constructor
 * @property {string} name The name of the person.
 */
function Person(name) {
    this.name = name;
}
```
Alternatively, instance properties can be documented as follows:
```javascript
/**
 * @class
 */
function Person(name) {
    /**
     * The name of the person.
     * @type {string}
     */
    this.name = name;
}
```
`@default defaultValue`

What is the default value of a parameter or instance property? For example:
```javascript
/** @constructor */
function Page(title) {
    /**
     * @default 'Untitled'
     */
     this.title = title || 'Untitled';
}
```

# Documenting Classes

JSDoc distinguishes between classes and constructors. The former concept is more like a type, while a constructor is one way of implementing a class. JavaScript’s built-in means for defining classes are limited, which is why there are many APIs that help with this task. These APIs differ, often radically, so you have to help JSDoc with figuring out what is going on. The following tags let you do that:

`@constructor`

Marks a function as a constructor.

`@class`

Marks a variable or a function as a class. In the latter case, @class is a synonym for @constructor.

`@constructs`

Records that a method sets up the instance data. If such a method exists, the class is documented there.

`@lends namePath`
Specifies to which class the following object literal contributes. There are two ways of contributing.
Records that a method sets up the instance data. If such a method exists, the class is documented there.
- @lends Person#: The object literal contributes instance members to Person.
- @lends Person: The object literal contributes static members to Person.

`@memberof parentNamePath`

The documented entity is a member of the specified object. @lends MyClass#, applied to an object literal, has the same effect as marking each property of that literal with @memberof MyClass#.
The most common ways of defining a class are: via a constructor function, via an object literal, and via an object literal that has an @constructs method.

#### DEFINING A CLASS VIA A CONSTRUCTOR FUNCTION
To define a class via a constructor function, you must mark the constructor function; otherwise, it will not be documented as a class. Capitalization alone does not mark a function as a constructor:
```javascript
/**
 * A class for managing persons.
 * @constructor
 */
function Person(name) {
}
```
#### DEFINING A CLASS VIA AN OBJECT LITERAL
To define a class via an object literal, you need two markers. First, you need to tell JSDoc that a given variable holds a class. Second, you need to mark an object literal as defining a class. You do the latter via the @lends tag:
```javascript
/**
 * A class for managing persons.
 * @class
 */
var Person = makeClass(
    /** @lends Person# */
    {
        say: function(message) {
            return 'This person says: ' + message;
        }
    }
);
```
#### DEFINING A CLASS VIA AN OBJECT LITERAL WITH AN @CONSTRUCTS METHOD
If an object literal has an @constructs method, you need to tell JSDoc about it, so that it can find the documentation for the instance properties. The documentation of the class moves to that method:
```javascript
var Person = makeClass(
    /** @lends Person# */
    {
        /**
         * A class for managing persons.
         * @constructs
         */
        initialize: function(name) {
            this.name = name;
        },
        say: function(message) {
            return this.name + ' says: ' + message;
        }
    }
);
```
If you omit the @lends, you must specify which class the methods belong to:
```javascript
var Person = makeClass({
        /**
         * A class for managing persons.
         * @constructs Person
         */
        initialize: function(name) {
            this.name = name;
        },
        /** @memberof Person# */
        say: function(message) {
            return this.name + ' says: ' + message;
        }
    }
);
```
#### SUBCLASSING
JavaScript has no built-in support for subclassing. When you subclass in your code (be it manually, be it via a library), you have to tell JSDoc what is going on:

`@extends namePath`

Indicates that the documented class is the subclass of another one. For example:
```javascript
/**
 * @constructor
 * @extends Person
 */
function Programmer(name) {
    Person.call(this, name);
    ...
}
// Remaining code for subclassing omitted
```
# Other Useful Tags
All of these tags are documented at the JSDoc website:

- Modularity: @module, @exports, @namespace
- Custom types (for virtual entities such as callbacks, whose signature you can document): @typedef, @callback
- Legal matters: @copyright, @license
- Various kinds of objects: @mixin, @enum
