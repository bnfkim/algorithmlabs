# ****FINDBEAD****

## 📍문제

### **문제**

---

모양은 같으나, 무게가 모두 다른 N개의 구슬이 있다. N은 홀수이며, 구슬에는 번호가 1,2,...,N으로 붙어 있다. 이 구슬 중에서 무게가 전체의 중간인 (무게 순서로 (N+1)/2번째) 구슬을 찾기 위해서 아 래와 같은 일을 하려 한다.

우리에게 주어진 것은 양팔 저울이다. 한 쌍의 구슬을 골라서 양팔 저울의 양쪽에 하나씩 올려 보면 어느 쪽이 무거운 가를 알 수 있다. 이렇게 M개의 쌍을 골라서 각각 양팔 저울에 올려서 어느 것이 무거운 가를 모두 알아냈다. 이 결과를 이용하여 무게가 중간이 될 가능성이 전혀 없는 구슬들은 먼저 제외한다.

예를 들어, N=5이고, M=4 쌍의 구슬에 대해서 어느 쪽이 무거운가를 알아낸 결과가 아래에 있다.

1. 구슬 2번이 구슬 1번보다 무겁다.
2. 구슬 4번이 구슬 3번보다 무겁다.
3. 구슬 5번이 구슬 1번보다 무겁다.
4. 구슬 4번이 구슬 2번보다 무겁다.

위와 같이 네 개의 결과만을 알고 있으면, 무게가 중간인 구슬을 정확하게 찾을 수는 없지만, 1번 구슬과 4번 구슬은 무게가 중간인 구슬이 절대 될 수 없다는 것은 확실히 알 수 있다. 1번 구슬보다 무거운 것이 2, 4, 5번 구슬이고, 4번 보다 가벼운 것이 1, 2, 3번이다. 따라서 답은 2개이다.

M 개의 쌍에 대한 결과를 보고 무게가 중간인 구슬이 될 수 없는 구슬의 개수를 구하는 프로그램을 작성하시오.

### **입력**

---

첫 줄은 구슬의 개수를 나타내는 정수 N(1 ≤ N ≤ 99)과 저울에 올려 본 쌍의 개수 M(0 ≤ M < N) 이 주어진다. 그 다음 M 개의 줄은 각 줄마다 두 개의 구슬 번호가 주어지는데, 앞 번호의 구슬이 뒤 번호의 구슬보다 무겁다는 것을 뜻한다.

### **출력**

---

첫 줄에 무게가 중간이 절대로 될 수 없는 구슬의 수를 출력 한다.

### **예제 입력**

```
5 4
2 1
4 3
5 1
4 2

```

### **예제 출력**

```
2

```

### **출처**

KOI 2003 중등부 1번

## 📍코드

```java
import org.w3c.dom.Node;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.StringTokenizer;

public class Main{
    static ArrayList<Integer>[] list, list2;
    static boolean[] visit; //방문여부 체크
    static int n, m, half;
    static int result,cnt = 0;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken()); //구슬의 개수
        m = Integer.parseInt(st.nextToken()); //쌍의 개수
        half = (n+1)/2; //구슬의 중간 무게

        list = new ArrayList[n+1];
        list2 = new ArrayList[n+1];
        visit = new boolean[n+1];

        //입력받기
        for(int i=1; i<=n; i++) {
            list[i] = new ArrayList<>();
            list2[i] = new ArrayList<>();
        }
        for(int i=0; i<m; i++){
            st = new StringTokenizer(br.readLine());
            int heavy = Integer.parseInt(st.nextToken());
            int light = Integer.parseInt(st.nextToken());
            list[heavy].add(light); // 2, 4, 5
            list2[light].add(heavy);
        }

        for(int i=1; i<=n; i++){
            System.out.println();
            System.out.println(">>> 큰 수 담은 리스트 dfs 시작");
            cnt = 0;
            dfs(i, true);

//            System.out.println("ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ ");
//
//            System.out.println(">>> 작은 수 담은 리스트 dfs 시작");
//            dfs(i,1, false);
        }

        System.out.println("ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ ");

        for(int i=1; i<=n; i++){
            System.out.println();
//            System.out.println(">>> 큰 수 담은 리스트 dfs 시작");
//            dfs(i,1, true);
//
//            System.out.println("ㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡㅡ ");

            System.out.println(">>> 작은 수 담은 리스트 dfs 시작");
            cnt = 0;
            dfs(i,false);
        }
        System.out.println(result);
    }

    /**
     * dfs로 진행해야함 -> 재귀함수 사용
     * 파라메터 ->
     * big
     * [2] - [1]
     * [4] - [3,2]
     * [5] - [1]
     * small
     * [1] - [2,5]
     * [2] - [4]
     * [3] - [4]
     */

    private static void dfs(int num, boolean isBigList) {
        System.out.println("숫자는 <" + num + "> 이 들어왔고, 현재 횟수는 <" + cnt + "> 입니다");
        if(isBigList){
            for(int node : list[num]){
                System.out.println("(큰수)" +num + " -> (작은수)" + node);
                cnt++;
                System.out.println(cnt + "만큼 연결되었습니다");
                if(half == cnt){
                    System.out.println("카운트가 " + half + "만큼 생겼습니다");
                    result +=1;
                    break;
                }
                dfs(node, true);
            }
        } else {
            for(int node : list2[num]){
                System.out.println("(작은수)" + num + " <- (큰수)" + node);
                cnt++;
                if(half == cnt){
                    System.out.println("카운트가 " + half + "만큼 생겼습니다");
                    result += 1;
                    break;
                }
                dfs(node, false);
            }
        }
    }
}
```

## 📍기록

- 중간이 ‘확실히’ 될 수 없는 조건을 생각할 것
    - 1) 나보다 작은 구슬이 3개 이상일 경우
    - 2) 나보다 큰 구슬이 3개 이상일 경우
