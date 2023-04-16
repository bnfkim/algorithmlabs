# ****NQUEEN****

## 📍문제

### **문제**

---

N-Queen 문제는 크기가 N × N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 문제이다.

N이 주어졌을 때, 퀸을 체스판에 놓는 방법의 수를 구하는 프로그램을 작성하시오.

### **입력**

---

첫째 줄에 체스판의 크기인 N이 주어진다. (1 ≤ N < 13)

### **출력**

---

첫째 줄에 N x N인 체스판 위에 N개의 퀸을 놓을 수 있는 방법의 수를 출력한다.

### **예제 입력**

```
8

```

### **예제 출력**

```
92

```

### **설명**

---

퀸은 체스판에서 직선, 대각선으로 거리에 상관없이 공격할 수 있는 기물이다.

## 📍코드

```java
import java.io.*;
import java.util.Arrays;

public class Main{
    static int n;
    static int[] chess;
    static int[] visit;
    static int result = 0;

    /** 생각의 발상을 해볼 것
     *  index  0 1 2 3
     *  arr   [2 0 3 1]
     *  => (0,2) (1,0) (2,3) (3,1) 이렇게 체스가 놓이는 경우다
     *  => 즉, 각 index = '열', 원소 값 = '행'
     */

    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        chess = new int[n];
        visit = new int[n];

        dfs(0);
        System.out.println(result);
    }
    public static void dfs(int depth){
        if(depth == n){ //마지막 열까지 갔다면, 종료
            result++;
            return;
        }
        for(int i=0; i<n; i++){
            chess[depth] = i;
            if (check(depth)) dfs(depth+1);
        }
    }
    public static boolean check(int col){
        for(int i=0; i<col; i++){
            if(chess[i] == chess[col]) {
                return false;
            } // 대각선상에 놓여있는 경우
              // = 열의 차와 행의 차가 같을 경우
            else if (Math.abs(col-i) == Math.abs(chess[col] - chess[i])) {
                return false;
            }
        }
        return true;
    }
}
```

## 📍기록

- 이차원 배열로 시도했다가 실패 …
- 실패한 코드 보기 …
    
    ```java
    import java.io.*;
    import java.util.Arrays;
    
    public class Main{
        static int n;
        static int[][] chess;
        static int[][] visit;
        static int result = 0;
    
        public static void main(String[] args) throws IOException {
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            n = Integer.parseInt(br.readLine());
            chess = new int[n][n];
            visit = new int[n][n];
    
            dfs(0);
            System.out.println(result);
        }
        /**
         *    👑x x x x
         *    x x o o o
         *    x o x o o
         *    x o o x o
         *    x o o o x
         *
         *      *    👑x x x x
         *      *    x x 👑o o
         *      *    x o x o o
         *      *    x o o x o
         *      *    x o o o x
         */
    
        /**
         * 퀸 특징 : 가로/세로/대각선 모두 잡을 수 있음
         * 1) 체스판에 0,0 으로 시작
         * 1-2) 가로/세로/대각선 모두 true 체크
         * 2) 그 다음 둘 수 있는 위치에 퀸 두기
         * 2-2) 가로/세로/대각선 모두 true 체크
         * 종료조건 : 퀸을 다 사용했을 때 정지 + result 증가
         */
        public static void dfs(int queen){
            if(queen == n+1) {
                System.out.println("queen 을 모두 소진하였습니다");
                result++;
                System.out.println();
                System.out.println("<<<< 지금까지 횟수 : " + result + ">>>>");
                System.out.println();
                return;
            }
    
            for(int i=0; i<n; i++){
                for(int j=0; j<n; j++){
                    if(visit[i][j] == 0){
                        //visit[i][j]++;
                        check(i, j, queen);
                        dfs(queen+1);
                        //visit[i][j]--;
                        unCheck(i, j, queen);
                    }
                }
            }
        }
        public static void check(int y, int x, int cnt){
            System.out.println("(" + x + "," + y +")에 " + cnt + "번째 퀸이 놓였습니다");
            //가로
            for(int i=0; i<n; i++) if(visit[y][i] == 0) visit[y][i] = cnt;
            //세로
            for(int i=0; i<n; i++) if(visit[i][x]==0) visit[i][x] = cnt;
            //대각선
            for(int i=0; i<n; i++){
                //왼쪽 + 위
                if(x-i>=0 && y-i>=0 && visit[x-i][y-i]==0) visit[x-i][y-i] = cnt;
                //오른쪽 아래
                if(x+i<n && y+i<n && visit[x+i][y+i]==0) visit[x+i][y+i] = cnt;
                //왼쪽 + 아래
                if(x-i>=0 && y+i<n && visit[x-i][y+i]==0) visit[x-i][y+i] = cnt;
                //오른쪽 + 위
                if(x+i<n && y-i>=0 && visit[x+i][y-i]==0) visit[x+i][y-i] = cnt;
            }
    
            for(int i=0;i<n;i++){
                for(int j=0;j<n;j++) System.out.print(visit[i][j] + " ");
                System.out.println();
            }
        }
    
        public static void unCheck(int y, int x, int cnt){
            System.out.println("(" + x + "," + y +")에 " + cnt + "번째 퀸을 뺍니다");
            for(int i=0; i<n; i++){
                for(int j=0; j<n; j++){
                    if(visit[i][j] == cnt) visit[i][j] = 0;
                }
            }
    //        //가로
    //        for(int i=0; i<n; i++) if(visit[y][i] == cnt) visit[y][i] = cnt-1;
    //        //세로
    //        for(int i=0; i<n; i++) if(visit[i][x] == cnt) visit[i][x] = cnt-1;
    //        //대각선
    //        for(int i=0; i<n; i++){
    //            //왼쪽 + 위
    //            if(x-i>=0 && y-i>=0 && visit[x-i][y-i]==cnt) visit[x-i][y-i]= cnt-1;
    //            //오른쪽 아래
    //            if(x+i<n && y+i<n && visit[x+i][y+i]==cnt) visit[x+i][y+i] = cnt-1;
    //            //왼쪽 + 아래
    //            if(x-i>=0 && y+i<n && visit[x-i][y+i]==cnt) visit[x-i][y+i]= cnt-1;
    //            //오른쪽 + 위
    //            if(x+i<n && y-i>=0 && visit[x+i][y-i]==cnt) visit[x+i][y-i]= cnt-1;
    //        }
    
            for(int i=0;i<n;i++){
                for(int j=0;j<n;j++) System.out.print(visit[i][j] + " ");
                System.out.println();
            }
        }
    }
    ```
    

- 일차원 배열로 생각하자

- 참고사이트
