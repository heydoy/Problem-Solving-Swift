# 깊이 우선 탐색 DFS
- 재귀를 이용하지 않고
```swift
func DFS(graph: [String: [String]], satrt: String) -> [String] {
    
    var visitedQueue: [String] = []
    var needVisitStack: [String] = []
    
    while !needVisitStack.isEmpty {
        let node: String = needVisitStack.removeLast()
        if visitedQueue.contains(node) { continue }
        
        visitedQueue.append(node)
        needVisitStack += graph[node] ?? []
    }
    
    return visitedQueue
}
```

- 재귀 이용해서
```swift
func practiceDFS(n lastNode: Int, edges: [(Int, Int)]) -> Int {
    var edgeInfo = [Int: Array<Int>]() // edgeInfo = [Int: [Int]]
    
    for edge in edges {
        print(edge)
        print("edfgoInfo[edge.0] = \(edgeInfo[edge.0])")
        if var array = edgeInfo[edge.0] {
            array.append(edge.1)
            edgeInfo[edge.0] = array
            print("if: \(edgeInfo), \(array)")
        } else {
            edgeInfo[edge.0] = [edge.1]
            print("else: \(edgeInfo), \(array)")
        }
    }
    
    var result = 0  // 탐색 횟수
    
    func dfs(node: Int, visited: [Int]) {
        print("dfs, node: \(node) / visited: \(visited)")
        
        guard node != lastNode else {   // 마지막 노드가 아니라면(전부 탐색)
            // 라스트 노드이면(전부 다 탐색했으면) 끝낸다.
            result += 1
            return
        }
        
        // neighbors가 없으면(인접 =노드가 없으면) 끝낸다.
        guard let neighbors = edgeInfo[node] else { return }
        
        for edge in neighbors {
            print("dfs, edge \(edge) / neighbors: \(neighbors), \(visited.contains(edge))")
            guard visited.contains(edge) == false else { continue }
            dfs(node: edge, visited: visited + [edge])
            
        }
        
    }
    dfs(node: 1, visited: [1])
    
    return result
}


//practiceDFS(n: 5, edges: [(1, 2), (1, 3), (1, 4), (2, 1), (2, 4), (2, 5), (3, 2), (3, 4), (4, 5)])

func exDFS(numbers: [Int], m: Int) {
    // 1. 궁극적으로 구하는 값: Subset 배열
    // 2. 재귀를 멈추는 조건: Subset의 원소 갯수가 m개가 되면 멈춘다.
    // 3. 재귀함수를 호출할 때의 초기 값: 어떤 원소라도 첫번째가 될 수 있도록.(고정하면 안됨)
    
    // 1
    var result: [[Int]] = []
    
    func dfs(selected: [Int]) {
        guard selected.count < m else {
            // 2. m 개가 되면 끝남
            result.append(selected)
            return
        }
        
        for number in numbers {
            guard selected.contains(number) == false else { continue }
            dfs(selected: selected + [number])
            }
        }
    
    // 3. 초기값
    dfs(selected: [])
    print(result)
}

//exDFS(numbers: [1, 2, 4], m: 2)

```
