# Go Interfaces

Go does support interfaces. In Go a method is a memeber of a type, not a class. A method can be attatched to a struct and enforced with an interface. The method signatures of the implementing struct has to be identical. If a custom struct has the matching name of an interface, then it must implement it in exactly the same way (has to have same number and type of arguments etc)

```Go
type animal interface {
    speak() string
}

type dog struct {
}

func (d dog) speak() string {
    return "Woof!"
}

type cat struct {
}

func (c cat) speak() string {
    return "Meow!"
}

type cow struct {
}

func (c cow) speak() string {
    return "Moo!"
}


func main() {
    poodle := animal(dog{}) // Cast dog to animal, if the cast works this indicates the relationship is intact
    fmt.Println(poodle)

    animals := []animal{dog{}, cat{}, cow{}}
    for _, animal := range animals {
        fmt.Println(animal.speak())
    }
}
```