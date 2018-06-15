extension Collection {
    subscript (safe index: Index) -> Element? {
        return indices.contains(index) ? self[index] : nil
    }
}

return nil if is out of range

to work with 2 dimensional array

ex.
m[1]?[2] ?? 0

