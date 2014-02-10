## Proprietà ed utilizzo degli Oggetti

In JavaScript tutto si comporta come un oggetto, ad eccezione di [`null`](#core.undefined) e [`undefined`](#core.undefined).


    false.toString(); // 'false'
    [1, 2, 3].toString(); // '1,2,3'

    function Foo(){}
    Foo.bar = 1;
    Foo.bar; // 1

Un malinteso comune è che i valori letterali numerici non possono essere
utilizzati come oggetti. La causa è da ritrovarsi in un difetto nel parser di
JavaScript, che interpreta il punto  della *dot notation* del numero come una
virgola di un numero decimale.

    2.toString(); // solleva SyntaxError

Ci sono un paio di soluzioni che possono essere utilizzate per
consentire ai letterali numerici di agire come oggetti.

    2..toString();  // il secondo punto è correttamente riconosciuto
    2 .toString();  // nota lo spazio a sinistra del punto
    (2).toString(); // 2 è valutato per primo

### Objects as a Data Type

Objects in JavaScript can also be used as [*Hashmaps*][1]; they mainly consist
of named properties mapping to values.

Using an object literal - `{}` notation - it is possible to create a
plain object. This new object [inherits](#object.prototype) from `Object.prototype` and
does not have [own properties](#object.hasownproperty) defined.

    var foo = {}; // a new empty object

    // a new object with a 'test' property with value 12
    var bar = {test: 12};

### Accessing Properties

The properties of an object can be accessed in two ways, via either the dot
notation or the square bracket notation.

    var foo = {name: 'kitten'}
    foo.name; // kitten
    foo['name']; // kitten

    var get = 'name';
    foo[get]; // kitten

    foo.1234; // SyntaxError
    foo['1234']; // works

The notations work almost identically, with the only difference being that the
square bracket notation allows for dynamic setting of properties and
the use of property names that would otherwise lead to a syntax error.

### Deleting Properties

The only way to remove a property from an object is to use the `delete`
operator; setting the property to `undefined` or `null` only removes the
*value* associated with the property, but not the *key*.

    var obj = {
        bar: 1,
        foo: 2,
        baz: 3
    };
    obj.bar = undefined;
    obj.foo = null;
    delete obj.baz;

    for(var i in obj) {
        if (obj.hasOwnProperty(i)) {
            console.log(i, '' + obj[i]);
        }
    }

The above outputs both `bar undefined` and `foo null` - only `baz` was
removed and is therefore missing from the output.

### Notation of Keys

    var test = {
        'case': 'I am a keyword, so I must be notated as a string',
        delete: 'I am a keyword, so me too' // raises SyntaxError
    };

Object properties can be both notated as plain characters and as strings. Due to
another mis-design in JavaScript's parser, the above will throw
a `SyntaxError` prior to ECMAScript 5.

This error arises from the fact that `delete` is a *keyword*; therefore, it must be
notated as a *string literal* to ensure that it will be correctly interpreted by
older JavaScript engines.

[1]: http://en.wikipedia.org/wiki/Hashmap

