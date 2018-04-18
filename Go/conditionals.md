# Go Conditional Logic and Loops

## If statements

Go if statements don't require parentheses around the boolean condition.

Simple if statement:

```Go
var x float64 = 42;
var result string

if x < 0 {
    result = "Less than zero"
} else if x == 0 {
    result = "Equal to zero"
} else { // Needs to be on the same line as the prior brace or it will error
    result = "Greater than zero"
}

fmt.Println("Result:", result)
```

You can declare variables as part of the intial if statement that are then local to it and eligible for GC after the statements finishes. Here `x` is set at the start of the if statement:

```Go
// var x float64 = 42;
var result string

if x:=42; x < 0 {
    result = "Less than zero"
} else if x == 0 {
    result = "Equal to zero"
} else { // Needs to be on the same line as the prior brace or it will error
    result = "Greater than zero"
}

// x is no longer accessible

fmt.Println("Result:", result)
```

## Switch statements

Go Switch statements can evaluate all types, not just constants or numerics. Additional cases are automatically jumped past when finding a match, unlike Java etc, no redundant break statements necessary!

```Go

rand.Seed(time.Now().Unix())
dow := rand.Intn(6) + 1
fmt.Println("Day", dow)

result := ""

switch dow {
    case 1:
        result = "It's Sunday!"
    case 7:
        result = "It's Saturday!"
    default:
        result = "It's a weekday!"
}

fmt.Println("Day", dow, ",", result)

// Conditional logic can be done at each case as well
switch {
    case dow == 1:
        result = "It's Sunday!"
    case dow == 7:
        result = "It's Saturday!"
    case dow > 1 && dow < 7:
        result = "It's a weekday!"
    default:
        result = "That's not a day"
}
```

Switches can also include a locally set variable as with an If statement. The `fallthrough` statement can be used to make the switch statement fall through as would happen in Java, basically the reverse of the `break` statement.

## Loops