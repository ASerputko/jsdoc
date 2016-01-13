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

