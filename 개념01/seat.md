## 📍문제

### **문제**

---

어떤 공연장에는 가로로 R개, 세로로 C개의 좌석이 R×C격자형으로 배치되어 있다. 각 좌석의 번호는 해당 격자의 좌표 (x,y)로 표시된다.

예를 들어보자. 아래 그림은 가로 7개, 세로 6개 좌석으로 구성된 7×6격자형 좌석배치를 보여주고 있다. 그림에서 각 단위 사각형은 개별 좌석을 나타내며, 그 안에 표시된 값 (x,y)는 해당 좌석의 번호를 나타낸다. 가장 왼쪽 아래의 좌석번호는 (1,1)이며, 가장 오른쪽 위 좌석의 번호는 (7,6)이다.

![https://alms-problem.s3.ap-northeast-2.amazonaws.com/seat1.png](https://alms-problem.s3.ap-northeast-2.amazonaws.com/seat1.png)

이 공연장에 입장하기 위하여 많은 사람이 대기줄에 서있다. 기다리고 있는 사람들은 제일 앞에서부터 1, 2, 3, 4, . 순으로 대기번호표를 받았다. 우리는 대기번호를 가진 사람들에 대하여 (1,1)위치 좌석부터 시작하여 시계방향으로 돌아가면서 비어있는 좌석에 관객을 순서대로 배정한다. 이것을 좀 더 구체적으로 설명하면 다음과 같다.

먼저 첫 번째 사람, 즉 대기번호 1인 사람은 자리 (1,1)에 배정한다. 그 다음에는 위쪽 방향의 좌석으로 올라가면서 다음 사람들을 배정한다. 만일 더 이상 위쪽 방향으로 빈 좌석이 없으면 오른쪽으로 가면서 배정한다. 오른쪽에 더 이상 빈자리가 없으면 아래쪽으로 내려간다. 그리고 아래쪽에 더 이상 자리가 없으면 왼쪽으로 가면서 남은 빈 좌석을 배정한다. 이 후 왼쪽으로 더 이상의 빈 좌석이 없으면 다시 위쪽으로 배정하고, 이 과정을 모든 좌석이 배정될 때까지 반복한다.

아래 그림은 7×6공연장에서 대기번호 1번부터 42번까지의 관객이 좌석에 배정된 결과를 보여주고 있다.

![https://alms-problem.s3.ap-northeast-2.amazonaws.com/seat2.png](https://alms-problem.s3.ap-northeast-2.amazonaws.com/seat2.png)

여러분은 공연장의 크기를 나타내는 자연수 R과 C가 주어져 있을 때, 대기 순서가 K인 관객에게 배정될 좌석 번호 (x,y)를 찾는 프로그램을 작성해야 한다.

### **입력**

---

첫 줄에는 공연장의 격자 크기를 나타내는 정수 R과 C가 하나의 공백을 사이에 두고 차례대로 주어진다. 두 값의 범위는 5 ≤ R, C ≤ 1,000이다. 그 다음 줄에는 어떤 관객의 대기번호 K가 주어진다. 단 1 ≤ K ≤ 100,000,000이다.

### **출력**

---

입력으로 제시된 대기번호 K인 관객에게 배정될 좌석번호 (x,y)를 구해서 두 값, x와 y를 하나의 공백을 사이에 두고 출력해야 한다. 만일 모든 좌석이 배정되어 해당 대기번호의 관객에게 좌석을 배정할 수 없는 경우에는 0(숫자 영)을 출력해야 한다.

### **예제 입력**

```
7 6
12

```

### **예제 출력**

```
7 6

```

### **출처**

---

KOI 2014 지역본선 고등부 1번, 중등부 1번, 초등부 2번

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
        StringTokenizer st = new StringTokenizer(br.readLine());
        int r = Integer.parseInt(st.nextToken()); //가로 -> 7
        int c = Integer.parseInt(st.nextToken()); //세로 -> 6
        int k = Integer.parseInt(br.readLine());

        int[][] arr = new int[r+1][c+1];
        int cnt = 1;
        // x 시작변수, y 시작변수, x 끝변수, y 끝 변수 4가지를 둬야함
        int a = 1;
        int b = 1;
        int x=r;
        int y=c;

        while (true) {
            for(int i=a; i<=y; i++){ //위로 올라가는 경우
                arr[a][i] = cnt++;
            }
            if(cnt>r*c) break;
            a++;
            for(int i=a; i<=x; i++) { //오른쪽으로 가는 경우
                arr[i][y] = cnt++;
            }
            if(cnt>r*c) break;
            y--;
            for(int i=y; i >=b; i--){ //아래로 내려가는 경우
                arr[x][i] = cnt++;
            }
            if(cnt>r*c) break;
            x--;
            for(int i=x; i>=a; i--){ //왼쪽으로 가는 경우
                arr[i][b] = cnt++;
            }
            if(cnt>r*c) break;
            b++;
        }
        if(k>r*c) System.out.println(0);
        else{
            for(int i=1; i<=r; i++){
                for(int j=1; j<=c; j++){
                    if(arr[i][j] == k) System.out.println(i + " " + j);
                }
            }
        }
    }
}
```

## 📍기록

- 처음 내가 시도했던 코드
    - 실패한 이유 → 안쪽으로 숫자가 잘 집어넣지지가 않음
    - 놓쳤던 부분 →  `x 시작변수, y 시작변수, x 끝변수, y 끝 변수 4가지를 둬야함`
    - 변수 4가지를 두고, 그 4가지를 서로 연관되게 섞어두면 되었을 것

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main{
    static int[][] arr;
    static int x, y;
    static int r, c, k;
    public static void check() {
        int cnt = 1;
        x = 1;
        y = 1;
        for(int i=0; i<c/2; i++){
            for(int j=0; j<c-i; j++){
                System.out.println("----1차 : x 그대로 + y 변경");
                if(cnt == k) {
                    x = i;
                    y = j;
                    return;
                }
                arr[c-j-1][i] = cnt++;
                System.out.println("cnt = " + cnt);

            }
            cnt -= 1;
            for(int j=0; j<r-i; j++){
                System.out.println("----2차 : x변경 + y는 그대로 ");
                if(cnt == k) {
                    x = j;
                    y = c-i-1;
                    return;
                }
                arr[i][j] = cnt++;

            }
            cnt -= 1;
            for(int j=0; j<c-i; j++){
                System.out.println("----3차 : x그대로");
                if(cnt == k){
                    x = r-i-1;
                    y = c-j;
                    return;
                }
                arr[j][r-i-1] = cnt++;
                System.out.println("cnt = " + cnt);
            }
            cnt -= 1;
            for(int j=0; j<r-(i+1); j++){
                System.out.println("----4차 : y그대로 + x변경");
                if(cnt == k){
                    x = j; // 6 ->
                    y = i; // 5 ->
                    return;
                }
                arr[c-i-1][r-j-1] = cnt++;
                System.out.println("cnt = " + cnt);
            }
            cnt -= 1;
        }
    }
    public static void main(String[] args) throws IOException {
        // Please Enter Your Code Here
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        r = Integer.parseInt(st.nextToken()); //가로 -> 7
        c = Integer.parseInt(st.nextToken()); //세로 -> 6
        k = Integer.parseInt(br.readLine());

        arr = new int[c][r];
        check();
        System.out.println();
        for(int i=0; i<c; i++){
            for(int j=0; j<r; j++){
                System.out.print(arr[i][j] + "   ");
            }
            System.out.println();
        }

        System.out.println((x+1) + " " + (y+1));
    }
}
```

- 해답이 다른 두 문제 참고

[[BAEKJOON 백준] 10157 자리배정](https://kunduz.tistory.com/entry/BAEKJOON-백준-10157-자리배정)

[[실전 문제] seat](https://ozofweird.tistory.com/entry/실전-문제-seat)
