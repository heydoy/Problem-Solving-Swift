# LinearSearch
```swift
func linearSearch(_ number: Int, _ array: [Int]) -> Int? {
    for (index, value) in array.enumerated() {
        if value == number{
            return index
        }
    }
    return nil
}

let myArray = [5, 2, 4, 7]
```
