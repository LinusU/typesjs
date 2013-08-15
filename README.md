```
 _                           _
| |                         (_)
| |_ _   _ _ __   ___  ___   _ ___ 
| __| | | | '_ \ / _ \/ __| | / __|
| |_| |_| | |_) |  __/\__ \_| \__ \
 \__|\__, | .__/ \___||___(_) |___/
      __/ | |              _/ |
     |___/|_|             |__/

```

`types.js` provides an easy, readable way to check types.

## Simple usage

Just pass a `value` and a `constructor`. You can also pass an `Array` of constructors.

If a `value` is null, or doesn't match a type, your function is safely halted. (Optional values are supported too!)

### Example 1
```js
// Simple checks.
t("Nick Cage", String); // Passes
t(1997, Number);        // Passes
t([], String);          // TypeError. Your code is safely halted.

t("ConAir", [String, Array]);                 // Passes
t([1989, "Vampire's Kiss"], [String, Array]); // Passes
t({category: "comedy"}, [String, Array]);     // TypeError
```

### Example 2
```js
// Let's add checks for a shared login method.

// Define variables.
var usernameStr = "NickCage",
    passwordStr = "winsatlife",
    ageNum      = "eternal"; // This should be a number, nobody is immortal... right?

// Execute function.
sharedLoginFunction(usernameStr, passwordStr, ageNum);

// Define function.
function sharedLoginFunction(usernameStr, passwordStr, ageNum) {
    // In this case, we don't want to move forward unless our parameters seem legit.
    t(usernameStr, String);
    t(passwordStr, String);
    t(ageNum, Number); // TypeError. Let us waste no more cycles on this function.

    // ...
}

```

## Advanced usage

Multiple types. Pass an `Array` of constructors.

```js
t("I am not a number.", [Number, String]);
```

Optional checks. You may pass *"optional"* or *false* as the third parameter.
This will allow *null* or *undefined* values.

```js
t(null, String, "optional");
t(void 0, String, "optional");
t(undefined, String, "optional");
```

Custom types. If you've got a reference to a type's `constructor`, you can test it!

```js
var CustomType = function() {
  // ...
};

var instance = new CustomType();

t(instance, CustomType);
```

Disable `types.js`, at any time.

```js
t.enabled = false;
```

Using Node? `typesjs` is available on NPM.

```js
var t = require("typesjs");
```