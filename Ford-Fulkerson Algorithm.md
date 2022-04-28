# **Ford-Fulkerson** Algorithm

## **Ford-Fulkerson Alg.** 
- **Ford-Fulkerson Algorithm**은 어떠한 흐름이 있는 네트워크에서, 시작점에서 종점까지의 흐름 중 최대값의 흐름을 계산하여 찾는 알고리즘이다. 위 알고리즘에서는 **최대 흐름 문제(Maximum flow problem)** 를 따르는데 이것에 대해 먼저 알아보자.

### - **최대 흐름 문제(Maximum flow problem)**
- 어떠한 방향 그래프 *G = <V, E>* 에서, 그래프의 간선(Edge)에는 가중치의 역할을 하는 유한한 용량이 있다고 하자. 그리고 이걸 편의상 **흐름 네트워크(flow network)** 라고 칭하자.
- 최대 흐름 문제를 나타내는 그래프 G에서는 시작점을 나타내는 노드 s(Source), 종점을 나타내는 노드 t(Sink)를 설정해줘야 한다.
- 이 문제를 보다 쉽게 이해하기 위해 다음 용어들을 정리해보았다.
    - 특정 값이 s와 t사이에서 흐르는데 그 양을 **유량 혹은 흐름(flow)** 이라 한다. <br/>
    - *[f / f(u, v)]*, 최대로 흐를 수 있는 양의 크기를 **용량(Capacity)** <br/> 이라 한다. *(※ u와 v는 임의의 정점!)*
    - *[c / c(u, v)]*, 유량을 보내는 길 혹은 통로를 **증가경로(Augmenting Path)** <br/> 라 한다.
    - 특정 상황에서 흐를 수 있는 최대의 유량을 **잔여용량(Residual Capacity)** 이라 한다.
- 최대 흐름 문제는 다음을 만족한다.
    - **용량 제약** <br/>
용량 제약 조건 : 그래프에 존재하는 여러 간선에 흐르는 유량은 항상 0보다 크거나 같고, 두 간선에서 흐르는 유량은 용량을 넘을 수 없다. <br/> 
        #### ※ *f(u, v) >= 0, f(u, v) <= c(u, v)* 
    - **유량의 대칭성** <br/>
유량의 대칭성 조건 : 특정 정점 u에서 v로 15만큼 유량이 흘렀다면, 그 반대인 경우에는 -15라고 볼 수 있다.
        #### ※ *f(u, v) = 15 <--> f(v, u) = -15* 
        - **Note!** s에서 출발한 flow가 정점 a에서 정점 b로 간선 ab를 따라 2만큼 흘렀다고 한다면, b에서 a만큼 역간선을 따라 -2만큼 흐른 것 과 같다.<br/>
    - **흐름의 보존** <br/>
보존 제약 조건 : 시점 s 혹은 종점 t를 제외한 그래프 상의 정점에서 흐르거나 들어오는 유량은 동일하다.
- 그래프 내에서 간선에 대한 유량 및 용량 표시는 다음과 같이 한다.<br/> *유량(flow) / 용량(capacity) = f(u, v) / c(u, v)*
- 그래프의 분석을 위해 **DFS(깊이 우선 탐색), BFS(너비 우선 탐색)** 를 사용하는데, *최대 흐름 문제*에서는 **깊이 우선 탐색**을 사용한다.
- 간단히 정리하자면 최대 흐름 문제(유량 네트워크)는 **그래프(네트워크)에서 유량이 최대로 얼마나 흐를 수 있는지 구하는 문제**라고 볼 수 있다.

### - **Ford-Fulkerson 알고리즘**
- 이제 **최대 흐름 문제(Maximum flow problem** or **flow network)** 에 대해 알아봤으니, **Ford-Fulkerson 알고리즘**이 **flow network**의 어떤 원리를 이용하여 알고리즘을 구성하는지 알아보도록 하자.
```
Ford-Fulkerson Alg.

1. 시점 s(Source)에서 종점 t(Sink)로 가는 증가 경로를 찾는다.
2. 증가 경로에서 유량(흐름)을 받을 수 있는 용량을 확인하고, 해당하는 경로의 최대치의 유량을 찾는다.
3. 그에 해당하는 유량을 흘러보낸다.
4. 위의 과정을 유량을 더 이상 흘려보낼 수 없을 때 까지 반복 후 종료한다.
```
더 쉽고 확실하게 이해를 하고자 직접 그림을 그려 Ford-Fulkerson Algorithm을 구현해보았다.


1) 이러한 방향 그래프 G=<V, E>가 있다고 하자.
<img width="900" alt="1" src="https://user-images.githubusercontent.com/68879690/165798513-5451698b-cccf-4d63-ad16-d0d68d31c15a.PNG">

2) s -> a -> c -> t 순서로 탐색하고, s -> b -> d -> t를 탐색한다. 순서는 상관이 없다.
<img width="900" alt="2" src="https://user-images.githubusercontent.com/68879690/165799072-cbbd8f02-5307-4754-8ae7-42d927ab7d84.PNG">

3) s에서 t까지 최대의 유량을 전달하는게 목적이므로, c에서 a로 역간선을 통해 유량을 역으로 흘려준다.
<img width="900" alt="3" src="https://user-images.githubusercontent.com/68879690/165799566-3425d3ae-f1c0-4098-a7f7-a2c627b91214.PNG">

4) 최종적으로 s에서 t까지 최대 유량이 전달된 것을 확인할 수 있으며, 알고리즘이 종료된다.
<img width="900" alt="4" src="https://user-images.githubusercontent.com/68879690/165799870-c34801cd-2302-4631-acdd-1e30396f9ab6.PNG">

p.s. 이해를 위해 직접 그린 이 그래프를 Ford-Fulkerson 알고리즘으로 나타내는 과정에서 복잡하거나 많은 수의 정점 및 간선이 없어서 최대값의 유량을 구하는 경로가 비교적 쉽고 다양했지만, 조금 더 복잡한 그래프 상에서는 구하는 경로도 조금 까다로울 것이고 매우 비효율적일 수도 있을 것 같다는 생각을 했다. 이에 대한 얘기는 뒤에서 마저 해보겠다.

### - **Ford-Fulkerson Algorithm** 코드 구현 (DFS)

```java
public static int capacity[][];
    public static int flow[][];
    public static int path[]; // 
    public static boolean visited[];
    public static LinkedList<Integer> graph[];

    public static boolean dfs(int start) {
        if (start == Sink) {
            return true;
        }

        visited[start] = true;
        LinkedList<Integer> nexts = graph[start];
        for (int next: nexts) {
            if ( !visited[next] && capacity[start][next] - flow[start][next] > 0) {
                path[next] = start;

                if (dfs(next)) { // 계속 경로를 찾고, 찾으면 탈출
                    return true;
                }
            }
        }
        return false;
    }

    // O((V+E)F)
    public static int FordFulkerson() {
        int total = 0;
        while (dfs(Source)) { // dfs로 경로 찾기(증가경로), 경로가 더이상 없으면 종료임.
            // 경로에서 흘릴수 있는 최대의 유량(flow)을 찾기
            int flowNum = Integer.MAX_VALUE;
            for(int i = Sink; i != Source; i = path[i]) {
                int from = path[i];
                int to = i;
                flowNum = Math.min(flowNum, (capacity[from][to]) - flow[from][to]);
            }
            // 찾은 경로에 유량을 흘려보내기. 역방향도 흘려주기.
            for(int i = Sink; i != Source; i = path[i]) {
                int from = path[i];
                int to = i;

                flow[from][to] += flowNum;
                flow[to][from] -= flowNum;
            }

            total += flowNum;

            // 찾은 경로를 초기화해서 dfs로 경로 찾기를 Source > Sink 까지 다시 할 수 있게 함.
            Arrays.fill(path, -1);
            Arrays.fill(visited, false);
        }
        return total;
    }

```

### 항상 Ford-Fulkerson이 정답일까?
- 위에서 짧게 언급했지만 Ford-Fulkerson을 너비 우선 탐색 방식으로 최대 흐름 문제를 해결하려고 하다보면 매우 비효율적인 상황에 직면할 수 있음을 느꼈다. 다음 예시를 통해 자세히 알아보자.

- 다음과 같은 그래프가 있다. B에서 C로 가는 간선의 유량과 용량이 1로 고정되어 있고, 나머지는 매우 큰 수로 되어있다.
<img width="900" alt="one" src="https://user-images.githubusercontent.com/68879690/165815887-d75b0d03-6a97-428f-9f8b-e674a8de43cb.PNG">

① A->B->C->D 경로 탐색 <br/>
② 역간선을 이용하여 A->C->B->D 경로 탐색 <br/>
③ 최대 유량 문제 해결을 위해 위 그래프에서 1000번의 루프 발생<br/>

* DFS을 통해 **Ford-Fulkerson의 시간복잡도는 O((V+E)F)** 임을 알 수 있다.
<img width="900" alt="two" src="https://user-images.githubusercontent.com/68879690/165818668-f32bc28d-5501-40d1-9bce-ea767dfc6957.PNG">


* DFS로 탐색했을 때, 엄청나게 많은 연산 횟수가 도출이 되었다. 이를 해결하기 위해 **BFS(너비 우선 탐색)** 방식을 사용하는 **Edmonds-Karp Algorithm** 을 사용한다.
    - 처음엔 DFS나 BFS나 큰 차이는 없을테지만, BFS는 정점을 기준으로 가장 빠른 증가 경로(Augmenting path)를 찾을 수 있다.
