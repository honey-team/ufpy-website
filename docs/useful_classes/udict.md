---
title: UDict[KT, VT, CDV]

tags:
  - useful class
---

# class UDict[KT, VT, CDV]

```py
class UDict(dictionary: AnyDict[KT, VT]) # (1)!
class UDict(dictionary: AnyDict[KT, VT], *, default: CDV)
class UDict(**kwargs: VT)
class UDict(*, default: CDV, **kwargs: VT)
```

1.  `AnyDict[KT, VT] = LikeDict[KT, VT] | dict[KT, VT]`. In UDict 

    !!! note
        `LikeDict[KT, VT]` is type which has `__getitem__`,
        `__setitem__`, `__delitem__` and `get()` methods. `UDict` is `LikeDict`.
    
    Read about [AnyDict](../type_checking/type_alias.md) and [LikeDict](../type_checking/protocols.md)

---

!!! note "UDict as generic"
    You can use `UDict` as `Generic`, because of it, there are 3 `TypeVar`s: KT, VT, CDV.

    KT and VT are key type and value type. In inbuilt `dict` there are KT and VT type vars.
    CDV is class default value.

    In this documentation KT, VT and CDV will be used in methods.

Create UDict object. If `default`, when not existent keys is given in
getting item, method will return `default`.

!!! example
    ```py
    d = UDict(hello=world, hi=python, default=10)
    ```

## (property, settable) dictionary: dict[KT, VT] { data-toc-label="dictionary" }

UDict's dictionary.

!!! example
    ```py
    print(d.dictionary)
    d.dictionary = {4: 'world'}
    ```

!!! tip
    You can use UDict to set dictionary

    !!! example
        ```py
        d.dictionary = UDict({1: 7})
        ```

## (property, settable) keys: list[KT] { data-toc-label="keys" }

UDict's keys

!!! example
    ```py
    print(d.keys)
    d.keys = [1, 2]
    ```

!!! tip
    You can use tuples to set keys
    
    !!! example
        ```py
        d.keys = 1, 2
        ```

## (property, settable) values: list[VT] { data-toc-label="values" }

UDict's values

!!! example
    ```py
    print(d.values)
    d.values = [7, 2]
    ```

!!! tip
    You can use tuples to set values
    
    !!! example
        ```py
        d.values = 7, 2
        ```

## (property, settable) items: list[tuple[KT, VT]] { data-toc-label="items" }

UDict's items.

!!! example
    ```py
    print(d.items)
    d.items = [(1, 7), (2, 2)]
    ```

!!! tip
    You can use tuples to set items or you can use tuples or lists with lists
    
    !!! example
        ```py
        d.items = (1, 7), (2, 2)
        d.items = [1, 7], [2, 2]
        ```

## (property, settable) default: CDV { data-toc-label="default" }

UDict's default value

!!! example
    ```py
    print(d.default)
    d.default = 'null'
    ```

## reverse() -> UDict[KT, VT, CDV] { data-toc-label="reverse()" }

Reverses UDict and returns it. (1)
{ .annotate }

1.  !!! question "How UDict is being reversing?"

        Just is being reversing items  
        `#!py u{'hello': 1, 'hi': 2}` -> `#!py u{'hi': 2, 'hello': 1}` (reversed)

!!! warning
    `#!py reverse()` edits UDict. If you don't want to reverse UDict use [`#!py reversed()`](#reversed-udictkt-vt-cdv) method instead.

!!! example
    ```py
    d.reverse()
    print(d) # prints reversed UDict
    ```

## reversed() -> UDict[KT, VT, CDV] { data-toc-label="reversed()" }

Returns reversed UDict

!!! example
    ```py
    print(d.reversed())
    ```

!!! tip "Get reversed UDict with inbuilt `#!py reversed()` and `#!py ~` operator"
    You can get reversed UDict with inbuilt `#!py reversed()` and with invert operator (`~`).
    !!! example
        ```
        print(~d)
        print(reversed(d))
        print(d.reversed() == reversed(d)) # True
        ```
    [Read more about `#!py reversed()` and `#!py ~` support in UDict](#__invert__-udictkt-vt-cdv)

## sort() -> UDict[KT, VT, CDV] { data-toc-label="sort()" }

Sorts UDict and returns it. (1)
{ .annotate }

1.  !!! question "How UDict is being sorting?"

        Just are being sorting items by keys.  
        `#!py u{'b': 1, 'a': 2}` -> `#!py u{'a': 2, 'b': 1}` (sorted)

!!! warning
    `#!py sort()` edits UDict. If you don't want to sort UDict use [`#!py sorted()`](#sorted-udictkt-vt-cdv) method instead.

!!! example
    ```py
    print(d.sort())
    ```

## sorted() -> UDict[KT, VT, CDV] { data-toc-label="sorted()" }

Returns sorted UDict

!!! example
    ```py
    print(d.sorted())
    ```

##  get() { data-toc-label="get(*, key, index, value, default)" }

```py
def get(*, key: KT) -> VT | CDV
def get(*, key: KT, default: DV) -> VT | DV
def get(*, index: int) -> VT | CDV
def get(*, index: int, default: DV) -> VT | DV
def get(*, value: VT) -> KT | CDV
def get(*, value: VT, default: DV) -> KT | DV
```

!!! failure "Using more than 1 argument"
    If you use 0 or 2 or 3 of this arguments (`key`, `index`, `value`), method will raise `ValueError`

Arguments:
#### `key: KT` { data-toc-label="key" }

UDict value's key to find.

!!! example
    ```py
    print(d.get(key='key')) # same that d['key']
    ```

#### `index: int` { data-toc-label="index" }

UDict value's index to find

!!! warning
    Indexes are starting from 1. Index of first element of UDict is 1.

!!! failure "`index` argument more than UDict length"
    If you use `index` argument make sure that `index` are less than UDict length. Otherwise `#!py get()`
    will raise `IndexError`

!!! example
    ```py
    print(d.get(index=2)) # second value of UDict
    ```

#### `value: VT` { data-toc-label="value" }

UDict key's value to find

!!! example
    ```py
    print(d.get(value=1)) # if d = UDict{'hello': 1}, this will be 'hello'
    ```

#### `default: DV` { data-toc-label="default" }

Default value, if the result was not found. If not provided, then `default` is `UDict.default` property.

!!! example
    ```py
    d = UDict(hello=1, hi=2, default=-1)
    print(d.get(key='hell')) # -1
    print(d.get(key='hell', default=None)) # None
    ```

## is_empty() -> bool { data-toc-label="is_empty()" }

Returns `True` if the UDict is empty (`len(UDict) == 0`), otherwise returns `False`.

!!! example
    ```py
        d = UDict(hello=1)
        d2 = UDict()
        print(d.is_empty()) # False
        print(d2.is_empty()) # True
    ```

!!! tip "Convert UDict to `#!py bool`"
    You can convert UDict to `#!py bool` or use UDict in `#!py if` statement. If `#!py UDict.is_empty() == True`
    then `#!py bool(UDict)` is False and by contrast. Same in `#!py if` because of `#!py if x` is the equivalent
    of `#!py if bool(x)`
    
    !!! example
        ```py
        # d is from code above
        print(bool(d)) # True
        if d:
            print("d is True") # d is True
        ```

## Magic methods

Currently, UDict supports all these magic methods:

### \_\_call\_\_(func: Callable[[KT, VT], VT]) -> UDict[KT, VT, CDV] { data-toc-label="\_\_call\_\_(func)" }

Returns new UDict, but all values generated with `func` function. First argument: key, second: value.

Arguments:
#### `func: (KT, VT) -> VT` { data-toc-label="func" }

First argument of function is key, second is value. Returns new value
    

!!! example
    ```py
    def f(k, v):
        return v * 2
    d = d(f) # multiply all values by 2
    ```

### \_\_neg\_\_() -> UDict[KT, int | float, CDV] { data-toc-label="\_\_neg\_\_()" }

Negates all values (if they support the `-` operator) to their opposite numbers.

!!! example
    ```py
    d = UDict(hello=1, hi=-2)
    print(-d) # u{'hello': -1, 'hi': 2}
    ```

### \_\_invert\_\_() -> UDict[KT, VT, CDV] { data-toc-label="\_\_invert\_\_()" }

The equivalent of [`#!py reversed()`](#reversed-udictkt-vt-cdv)

!!! example
    ```py
    print(~d)
    ```

### \_\_reversed\_\_() -> UDict[KT, VT, CDV] { data-toc-label="\_\_reversed\_\_()" }

The equivalent of [`#!py reversed()`](#reversed-udictkt-vt-cdv)

!!! example
    ```py
    print(reversed(d))
    ```

### \_\_getitem\_\_(key: KT | int | slice) -> UDict[KT, VT, DV] | VT { data-toc-label="\_\_getitem\_\_(key)" }

Returns the value for a single key, or a UDict for multiple keys provided with a slice.

!!! warning "Indexes starting at 1."

Arguments:
#### `key: KT | int | slice` { data-toc-label="key" }

Value's key or index to get or values's indexes slice to get.

!!! example
    ```py
    print(d['hello'])
    print(d[1:2])
    ```

!!! tip "Using indexes"
    You can also use indexes in `#!py __getitem__()`.

    !!! failure
        Keep in mind that indexes are using after the keys with the given value were not found.
        !!! example
            If you have `#!py 1` key, `d[1]` syntax will use `#!py 1` how key, not index. If you want to use index in
            all ways, use [`#!py get()`](#get) instead.
    
    !!! example
        ```py
        d = UDict(hello=1, hi=9)
        print(d[2]) # 9
        ```

### \_\_setitem\_\_(key: KT | int | slice, value: VT | list[VT] | tuple[VT]) { data-toc-label="\_\_setitem\_\_(key, value)" }

Sets the value or values for the given key or keys.

#### `key: KT | int | slice` { data-toc-label="key" }

Value's key or keys to set. This argument is the same with [`key` argument in `#!py __getitem__()` method](#key-kt-int-slice)

#### `value: VT | list[VT] | tuple[VT]` { data-toc-label="value" }

Value or values to set.

!!! example
    ```py
    d = UDict(hello=2, hi=1)
    d[2] = 'hello'
    print(d['hi']) # 'hello'
    d[:] = 'hello', 'world'
    print(d) # u{'hello': 'hello', 'hi': 'world'}
    ```

### \_\_delitem\_\_(key: KT | int | slice) { data-toc-label="\_\_delitem\_\_(key)" }

Deletes items with the given key or keys.

#### `key: KT | int | slice` { data-toc-label="key" }

Item's key or keys to delete. This argument is the same with [`key` argument in `#!py __getitem__()` method](#key-kt-int-slice).

### \_\_len\_\_() -> int { data-toc-label="\_\_len\_\_()" }

Returns the length of the UDict.

!!! example
    d = UDict(hello=1, hi=2)
    print(len(d)) # 2

### \_\_iter\_\_() -> Iterator[tuple[KT, VT]] { data-toc-label="\_\_iter\_\_()" }

Iterate over the UDict. The equivalent of `#!py items.__iter__()`.

!!! example
    ```py
    for k, v in d:
        print(f"Key: {k}\nValue: {v}") # Prints all keys and its values.
    ```

### \_\_bool\_\_() -> bool { data-toc-label="\_\_bool\_\_()" }

Returns whether the UDict is not empty. The equivalent of `#!py not is_empty()`

!!! example
    ```py
    print(bool(d))
    if d:
        print("D is not empty!")
    ```

### \_\_contains\_\_(item: tuple[KT, VT] | list[KT | VT] | KT) -> bool { data-toc-label="\_\_contains\_\_(item)" }

Checks whether the item or key is in the UDict.

Arguments:
#### item: tuple[KT, VT] | list[KT | VT] | KT { data-toc-label="item" }
Item or item's key.

!!! example
    ```py
    if ('key', 'value') in d: ...
    if ['key', 'value'] in d: ...
    if 'key' in d: ...
    ```

### \_\_repr\_\_() -> str { data-toc-label="\_\_repr\_\_()" }

Returns the string representation of the UDict. This allows the UDict to be used in `print()` and `repr()`.

!!! example
    ```py
    d = UDict(hello=1)
    print(d) # u{'hello': 1}
    print(repr(d)) # Same
    ```

### \_\_hash\_\_() -> int { data-toc-label="\_\_hash\_\_()" }

Returns the hash for `#!py repr(UDict)`. The equivalent of `#!py repr(UDict).__hash__()`.

### \_\_cmp\_\_(other: dict[KT, VT] | UDict[KT, VT, CDV]) -> int { data-toc-label="\_\_cmp\_\_(other)" }

Used by `#!py @cmp_generator`, which generates comparison magic methods like `==`, `!=`, `>`, `>=`, `<`, `<=` operators.

Comparing UDicts involves comparing their lengths, except for `#!py __eq__()`.

!!! example
    ```py
    d = UDict(hello=1)
    d2 = UDict(hello=1, hi=2)
    print(d != d2) # True
    print(d < d2) # True
    print(d > d2) # False
    ```

### \_\_eq\_\_(other: dict[KT, VT] | UDict[KT, VT, CDV]) -> bool { data-toc-label="\_\_eq\_\_(other)" }

Checks whether UDicts are the same. (Overrides generated by `#!py @cmp_generator` magic method)

!!! example
    ```py
    d = UDict(hello=1)
    d2 = UDict(hello=1, hi=2)
    print(d == d2) # False
    print(d == d) # True
    ```

!!! tip
    You can use dict to compare with UDict. Method will automatically generate UDict from this dict
    ```py
    print(d == {'hello': 1}) # True
    ```

### \_\_add\_\_(other: dict[KT, VT] | UDict[KT, VT, CDV]) -> UDict[KT, VT, CDV] { data-toc-label="\_\_add\_\_(other)" }

Adds the dictionary or UDict's dictionary to the UDict's dictionary. This method also has `r` and `i` versions (`+=`).

!!! example
    ```py
    print(d + {'hi': 2})
    print({'hi': 2} + d)
    d += {'hi': 2}
    ```

*[KT]: Key type
*[VT]: Value type
*[CDV]: Class default value

### \_\_sub\_\_(other: dict[KT, VT] | UDict[KT, VT, CDV]) -> UDict[KT, VT, CDV] { data-toc-label="\_\_sub\_\_(other)" }

Subtracts the dictionary or UDict's dictionary from the UDict's dictionary. This method also has `r` and `i` versions (`-=`).

!!! example
    ```py
    d = UDict(hello=1, hi=2)
    print(d - {'hello': 1}) # u{'hi': 2}
    d -= {'hello': 1}
    print(d) # Same
    ```

### \_\_mul\_\_(other: dict[KT, float | int] | UDict[KT, float | int, DV] | float | int) -> UDict[KT, SupportsMul, CDV] { data-toc-label="\_\_mul\_\_(other)" }

Multiply all values by `other`, if `other` is `#!py int` or `#!py float`.
Multiply values with keys equals to `other` keys by `other` values, if `other` is `#!py dict` or UDict.
This method also have `r` and `i` version (`*=`)

!!! warning
    Make sure that your UDict's values supports multiply operator (`*`)

!!! example
    ```py
    d = UDict(hello=1, hi=2)
    print(d * 2) # {'hello': 2, 'hi': 4}
    print(d * {'hi': 3}) # {'hello': 1, 'hi': 6}
    ```

### \_\_truediv\_\_(other: dict[KT, float | int] | UDict[KT, float | int, DV] | float | int) -> UDict[KT, SupportsTrueDiv, CDV] { data-toc-label="\_\_truediv\_\_(other)" }

Same that [`__mul__()`](#__mul__other-dictkt-float-int-udictkt-float-int-dv-float-int-udictkt-supportsmul-cdv),
but with divide operator (`/`).

!!! warning
    Make sure that your UDict's values supports divide operator (`/`)

!!! example
    ```py
    d = UDict(hello=1, hi=2)
    print(d / 2) # {'hello': 0.5, 'hi': 1}
    print(d / {'hi': 4}) # {'hello': 1, 'hi': 0.5}
    ```
