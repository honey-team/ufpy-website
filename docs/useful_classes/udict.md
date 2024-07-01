---
title: UDict

tags:
  - useful class
---

# `UDict` class

!!! note "UDict as generic"
    You can use `UDict` as `Generic`, because of it, there are 3 `TypeVar`s: KT, VT, CDV.

    KT and VT is key type and value type. In inbuilt `dict` there are KT and VT type vars.
    CDV is class defaul value.

    In this documentation KT, VT and CDV will be using in methods.

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

## (property, settable) keys: list[KT]

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

## (property, settable) values: list[VT]

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

## (property, settable) items: list[tuple[KT, VT]]

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

## (property, settable) default: CDV

UDict's default value

!!! example
    ```py
    print(d.default)
    d.default = 'null'
    ```

## reverse() -> UDict[KT, VT, CDV]

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

## reversed() -> UDict[KT, VT, CDV]

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

## sort() -> UDict[KT, VT, CDV]

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

## sorted() -> UDict[KT, VT, CDV]

Returns sorted UDict

!!! example
    ```py
    print(d.sorted())
    ```

##  get()

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
#### `key: KT`

UDict value's key to find.

!!! example
    ```py
    print(d.get(key='key')) # same that d['key']
    ```

#### `index: int`

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

#### `value: VT`

UDict key's value to find

!!! example
    ```py
    print(d.get(value=1)) # if d = UDict{'hello': 1}, this will be 'hello'
    ```

#### `default: DV`

Default value, if the result was not found. If not provided, then `default` is `UDict.default` property.

!!! example
    ```py
    d = UDict(hello=1, hi=2, default=-1)
    print(d.get(key='hell')) # -1
    print(d.get(key='hell', default=None)) # None
    ```

## is_empty() -> bool

`#!py True` if `len(UDict) == 0` else `#!py False`

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

### _\_call__(func: Callable[[KT, VT], VT]) -> UDict[KT, VT, CDV]

Returns new UDict, but all values generated with `func` function. First argument: key, second: value.

Arguments:
#### `func: (KT, VT) -> VT`

First argument of function is key, second is value. Returns new value
    

!!! example
    ```py
    def f(k, v):
        return v * 2
    d = d(f) # multiply all values by 2
    ```

### _\_neg__() -> UDict[KT, int | float, CDV]

Does all values (if they support `-` operator) to they's opposite numbers.

!!! example
    ```py
    d = UDict(hello=1, hi=-2)
    print(-d) # u{'hello': -1, 'hi': 2}
    ```

### _\_invert__() -> UDict[KT, VT, CDV]

The equivalent of [`#!py reversed()`](#reversed-udictkt-vt-cdv)

!!! example
    ```py
    print(~d)
    ```

### _\_reversed__() -> UDict[KT, VT, CDV]

The equivalent of [`#!py reversed()`](#reversed-udictkt-vt-cdv)

!!! example
    ```py
    print(reversed(d))
    ```

### _\_getitem__(key: KT | int | slice) -> UDict[KT, VT, DV] | VT

Returns value for one key, or UDict for multiply keys provided with slice.

Arguments:
#### `key: KT | int | slice`

Value's key or index to get or values's indexes slice to get.

!!! example
    ```py
    print(d['hello'])
    ```

!!! tip "Using indexes and slices"
    You can use indexes and slices in `#!py __getitem__()`.

    !!! warning "Indexes starting at 1."

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
    
    Slices can be used only with indexes. If slice is provided, method will return part of UDict from `start` index to
    `end` index with `step`.

    !!! example
        ```py
        d = UDict(hello=1, hi=3, world=9, ufpy=2)
        print(d[:3]) # u{'hello': 1, 'hi': 3, 'world': 9}
        print(d[2:3]) # u{'hi': 3, 'world': 9}
        print(d[:3:2]) # u{'hello': 1, 'world': 9}
        ```

### _\_setitem__(key: KT | int | slice, value: VT | list[VT] | tuple[VT])

Sets value or values to given key or keys.

#### `key: KT | int | slice`

Value's key or keys to set. This argument is the same with [`key` argument in `#!py __getitem__()` method](#key-kt-int-slice)

#### `value: VT | list[VT] | tuple[VT]`

Value or values to set.

!!! example
    ```py
    d = UDict(hello=2, hi=1)
    d[2] = 'hello'
    print(d['hi']) # 'hello'
    d[:] = 'hello', 'world'
    print(d) # u{'hello': 'hello', 'hi': 'world'}
    ```

### _\_delitem__(key: KT | int | slice)

Deletes items with given key or keys

#### `key: KT | int | slice`

Item 's key or keys to delete. This argument is the same with [`key` argument in `#!py __getitem__()` method](#key-kt-int-slice)

### _\_len__() -> int

Returns length of UDict

!!! example
    d = UDict(hello=1, hi=2)
    print(len(d)) # 2

### _\_iter__() -> Iterator[tuple[KT, VT]]

Iterate UDict. The equivalent of `#!py items.__iter__()`.

!!! example
    ```py
    for k, v in d:
        print(f"Key: {k}\nValue: {v}") # Prints all keys and its values.
    ```

### _\_bool__() -> bool

Returns that UDict is not empty. The equivalent of `#!py not is_empty()`

!!! example
    ```py
    print(bool(d))
    if d:
        print("D is not empty!")
    ```

*[KT]: Key type
*[VT]: Value type
*[CDV]: Class default value
