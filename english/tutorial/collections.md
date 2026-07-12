---
icon: list
---

# Collections

A collection variable starts with `&` and stores an ordered list of values. Collections are useful for inventories, map objects, configuration data, and any list that is not specifically a player value.

Player values use `@` instead. Use player methods such as `Take`, `Except`, and `Join` for groups of players.

## Create a collection

`Coll.Create` returns an empty collection:

```ser
&messages = Coll.Create
```

Add values with `Coll.Insert`:

```ser
Coll.Insert &messages "First message"
Coll.Insert &messages "Second message"
Coll.Insert &messages 42
```

A collection may hold different value types, but keeping similar values together usually makes a script easier to understand.

## Read values

`Coll.Fetch` uses indexes starting at 1:

```ser
$firstMessage = Coll.Fetch &messages 1
Print $firstMessage
```

Check the length before fetching an index that may not exist:

```ser
if {&messages -> length} >= 2
    Print {Coll.Fetch &messages 2}
end
```

Use `Coll.Contains` to check for a value:

```ser
if {Coll.Contains &messages "First message"}
    Print "The message exists."
end
```

## Iterate over a collection

Use `over` with a variable whose prefix matches the collection's values:

```ser
over &messages with $message $index
    Print "Message {$index}: {$message}"
end
```

Collections of references require a `*` loop variable:

```ser
&doors = GetFromMap doors

over &doors with *door
    CloseDoor *door
end
```

The optional second variable contains the current index, starting at 1.

## Remove values

Remove matching values:

```ser
Coll.Remove &messages "First message"
```

Remove a value at a specific index:

```ser
Coll.RemoveAt &messages 1
```

`Coll.Remove` removes every matching value by default. Its optional third argument limits how many matches are removed.

## Combine collections

`Coll.Join` returns a new collection containing all supplied collections:

```ser
&first = Coll.Create
&second = Coll.Create
Coll.Insert &first "A"
Coll.Insert &second "B"

&combined = Coll.Join &first &second
```

`Coll.Subtract` returns values from the first collection that are not present in the later collections:

```ser
&remaining = Coll.Subtract &combined &second
```

These returning methods do not modify their input collections.

## Collections returned by methods and properties

Some methods return collections directly:

```ser
&rooms = GetFromMap rooms
```

Some properties do the same:

```ser
&inventory = @sender -> inventory
```

Use `serhelp MethodName` or `serhelp properties player` to confirm the contained value type before choosing the loop variable prefix.

## Common mistakes

- Collection indexes start at 1, not 0.
- `Coll.Insert` modifies an existing collection; it does not return a new one.
- Inserting a collection nests it. Use `Coll.Join` to combine collection contents.
- The variable after `with` must match the contained type.
- Use `@` player values for groups of players, not a generic collection.

### What's next?

Continue with [Memory scopes](memory-scopes.md) to control how long variables exist.
