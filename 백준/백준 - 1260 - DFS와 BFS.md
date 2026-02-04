백준 - 1260 - DFS와 BFS

https://www.acmicpc.net/problem/1260

모르는 개념이라 ai와 같이 했다 
gemini
https://gemini.google.com/share/3691befff708

다시 복습하기.


```java
import java.io.*;  
import java.util.*;  
  
public class Main {  
    public static boolean[] visited; // DFS/BFS 수행 시 방문 여부를 기록할 배열  
    public static ArrayList<Integer>[] adj; // 각 정점의 연결 상태를 저장할 리스트 배열  
    public static StringBuilder sb = new StringBuilder();  
    public static Queue<Integer> q = new LinkedList<>();  
  
  
    public static void main(String[] args) throws IOException {  
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));  
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));  
  
  
        //NMV 입력  
        StringTokenizer st = new StringTokenizer(br.readLine());  
        int N = Integer.parseInt(st.nextToken());  
        int M = Integer.parseInt(st.nextToken());  
        int V = Integer.parseInt(st.nextToken());  
  
        adj = new ArrayList[N+1];  
        visited = new boolean[N+1];  
  
        for (int i = 1; i < N+1; i++) {  
            adj[i] = new ArrayList<>();  
        }  
        // 각 정점마다 연결된 친구들을 담을 준비가 끝  
  
        for (int i = 0; i < M; i++) {  
            //간선 정보를 입력한다. 각 정점에.  
            // node 연결 상태 입력  
            StringTokenizer nodes = new StringTokenizer(br.readLine());  
            int nd1 = Integer.parseInt(nodes.nextToken());  
            int nd2 = Integer.parseInt(nodes.nextToken());  
            adj[nd1].add(nd2);  
            adj[nd2].add(nd1);  
        }  
  
        // 노드정렬  
        for (int i = 1; i < N+1; i++) {  
            Collections.sort(adj[i]);  
        }  
  
        //DFS 탐색  
        dfs(V);  
        sb.append('\n');  
  
        //BFS 탐색  
        // visited 초기화  
        Arrays.fill(visited, false);  
  
        bfs(V);  
  
  
        //출력  
        bw.write(sb.toString());  
        bw.flush();  
        bw.close();  
        br.close();  
    }  
    public static void bfs(int v) {  
        q.add(v);  
        visited[v] = true;  
  
        while (!q.isEmpty()) {  
            int polled = q.poll();  
            sb.append(polled).append(' ');  
  
            for (int adjnode : adj[polled]) {  
                if(!visited[adjnode]) {  
                    q.add(adjnode);  
                    visited[adjnode] = true;  
                }  
            }  
        }  
    }  
  
    public static void dfs(int v) {  
        visited[v] = true;  
        sb.append(v).append(' ');  
        for (int next : adj[v]) {    
            if(!visited[next]) {  
                dfs(next);  
            }  
        }  
    }  
  
  
}
```


