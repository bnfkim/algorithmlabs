# ****attackrange****

## 📍문제

### **문제**

---

윤성이는 어렸을 적부터 수없이 몰려오는 적으로부터 기지를 방어하는 디펜스 유형의 게임을 플레이하는 것을 좋아했다. 그래서 간단한 디펜스 게임을 만들어 보려고 한다.

당신은 윤성이를 도와, 디펜스 게임 내에서 플레이어가 설치하는 유닛의 사거리를 나타내는 기능을 구현하면 된다.

### **입력**

---

입력 첫째 줄에는 디펜스 게임의 맵 크기 N이 주어딘다. 맵은 N×N 크기의 2차원 형태이다. (N은 6이상 100이하의 짝수)

둘째 줄에는 유닛이 설치될 위치 X, Y와 유닛의 사거리 R이 주어진다. X는 행의 번호, Y는 열의 번호를 의미한다. (X, Y는 1이상 N이하의 자연수, R은 N/2이하의 자연수)

### **출력**

---

예제 출력과 같이 유닛의 사거리를 나타내어 출력한다. (유닛의 사거리가 아무리 길어도 맵을 벗어날 수는 없다.)

### **예제 입력**

```
8
4 5 3

```

### **예제 출력**

```
0 0 0 0 3 0 0 0
0 0 0 3 2 3 0 0
0 0 3 2 1 2 3 0
0 3 2 1 x 1 2 3
0 0 3 2 1 2 3 0
0 0 0 3 2 3 0 0
0 0 0 0 3 0 0 0
0 0 0 0 0 0 0 0

```

### **예제 입력**

```
6
2 3 3

```

### **예제 출력**

```
3 2 1 2 3 0
2 1 x 1 2 3
3 2 1 2 3 0
0 3 2 3 0 0
0 0 3 0 0 0
0 0 0 0 0 0

```

## 📍코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main{
    public static void main(String[] args) throws IOException {
        // Please Enter Your Code Here
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int[][] arr = new int[N+1][N+1];
        StringTokenizer st = new StringTokenizer(br.readLine());
        int X = Integer.parseInt(st.nextToken());
        int Y = Integer.parseInt(st.nextToken());
        int R = Integer.parseInt(st.nextToken());

        for(int i=1; i<=R; i++){
            for(int j=0; j<=i; j++){
                if((X-i+j) > 0 && (Y+j) <= N) arr[X-i+j][Y+j] = i; //위+오른
                if((X-j)>0 && (Y-i+j) > 0) arr[X-j][Y-i+j] = i; //위+왼
                if((X+i-j)<=N && (Y-j)>0) arr[X+i-j][Y-j] = i; //아래+왼
                if((X+j) <=N && (Y+i-j <= N) )arr[X+j][Y+i-j] = i; //아래+오른
            }
        }
        for(int i=1; i<=N; i++){
            for(int j=1; j<=N; j++){
                if(i == X && j == Y) System.out.print("x ");
                else {
                    System.out.print(arr[i][j] + " ");
                }
            }
            System.out.println();
        }
    }
}
```

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main{
    public static void main(String[] args) throws IOException {
        // Please Enter Your Code Here
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int N = Integer.parseInt(br.readLine());
        int[][] arr = new int[N][N];
        StringTokenizer st = new StringTokenizer(br.readLine());
        int X = Integer.parseInt(st.nextToken())-1;
        int Y = Integer.parseInt(st.nextToken())-1;
        int R = Integer.parseInt(st.nextToken());

        for(int i=0; i<N; i++){
            for(int j=0; j<N; j++){
                int dist = Math.abs(Y-j) + Math.abs(X-i);
                if(dist == 0) arr[i][j] = -1;
                else if(dist<=R) arr[i][j] = dist;
            }
        }
        for(int i=0; i<N; i++){
            for(int j=0; j<N; j++){
                if(arr[i][j] == -1) System.out.print("x ");
                else {
                    System.out.print(arr[i][j] + " ");
                }
            }
            System.out.println();
        }
    }
}
```

## 📍기록

- 하나하나 적어보면서 그 안에서 루틴을 찾으려고 노력함

```java
//i=2
arr[X][Y-2] = 2; //왼쪽
arr[X-1][Y-1] = 3; //왼쪽위
arr[X-0][Y-2+0] = 2; //왼쪽
arr[X-0-1][Y-2+1] = 3; //왼쪽위

arr[X-2][Y+0] = 3; // 위쪽
arr[X-1][Y+1] = 3; // 위오른
arr[X-2+0][Y+0+0] = 3; // 위쪽
arr[X-2+1][Y+0+1] = 3; // 위오른

arr[X+0][Y+2] = 2; //오른쪽
arr[X+1][Y+1] = 3; //오른쪽아래
arr[X+1][Y+2-1] = 3; //오른쪽아래

arr[X+2][Y-0] = 3; //아래
arr[X+1][Y-1] = 3; //아래왼

//i=3,
arr[X-0][Y-3] = 3; //왼쪽
arr[X-1][Y-2] = 3; //왼쪽위대각선
arr[X-2][Y-1] = 3; //왼쪽위대각선

arr[X-3][Y+0] = 3; // 위쪽
arr[X-2][Y+1] = 3; // 위오른
arr[X-1][Y+2] = 3; // 위오른

arr[X+0][Y+3] = 3; //오른쪽
arr[X+1][Y+2] = 3; //오른쪽아래 
arr[X+2][Y+1] = 3; //오른쪽아래

arr[X+3][Y-0] = 3; //아래
arr[X+2][Y-1] = 3; //아래왼
arr[X+1][Y-2] = 2; //아래왼
```

- 참고 : 거리를 이용하는 방식
