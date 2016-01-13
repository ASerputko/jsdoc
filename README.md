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

