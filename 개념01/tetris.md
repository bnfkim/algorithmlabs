# ****tetris****

## 📍문제

### **문제**

---

테트리스를 해본 사람이라면 작대기 모양 테트리미노가 나오길 간절히 기다렸던 적이 있을 것이다. 지금 윤성이가 그러하다. 기다리고 기다리던 작대기 모양 테트리미노가 드디어 나온 것이다.

테트리스 맵은 가로로 C칸, 세로로 R칸의 C×R격자형 모양이다. 예를 들어보자. 아래 그림은 가로가 6칸, 세로가 6칸인 테트리스 맵의 상태이다.

![https://alms-problem.s3.ap-northeast-2.amazonaws.com/TetrismapEx.jpg](https://alms-problem.s3.ap-northeast-2.amazonaws.com/TetrismapEx.jpg)

(검정색 칸은 이미 메워져있던 칸이고, 회색칸은 이번에 메울 작대기 모양 테트리미노를 의미한다.)

이때 가로가 1칸이고 세로가 4칸인 1×4 직사가형 작대기 모양의 테트리미노(테트리미노는 항상 1×4)를 왼쪽에서 5번째 칸에 둘 경우 총 세줄의 수평선을 메울 수 있다. 테트리스는 한번에 여러 수평선을 메울수록 큰 점수를 얻는 게임이므로, 위 경우에서는 이 방법이 가장 높은 점수를 얻을 수 있는 방법이다.

윤성이를 도와 작대기 모양 테트리미노를 어디에 두었을 때 가장 높은 점수를 얻을 수 있는지 알려주자. (윤성이는 작대기 모양 테트리미노가 나왔을때 게임오버를 당할지언정 가로가 더 길도록 눕혀서 두지 않는다는 나름의 테트리스 철학이 있다.)

그리고 테트리스는 무조건 일자로 떨어진다. (오른쪽에서 왼쪽으로 공간을 비집고 들어가는 등의 스킬은 윤성이에겐 존재하지않는다.)

### **입력**

---

첫 줄에는 격자 크기를 나타내는 정수 C와 R이 하나의 공백을 사이에 두고 차례대로 주어진다. 두 값의 범위는 5 ≤ C, R ≤ 20이다. 그다음 줄 부터 총 R줄에 걸쳐 맵의 상태를 나타내는 숫자들이 공백을 사이에 두고 주어진다. 0은 아직 채워지지 않은 칸을 나타내며 1은 채워져있는 칸을 나타낸다.

### **출력**

---

작대기를 왼쪽에서 X번째 자리에 두었을 때 가장 높은 점수를 얻을 수 있고 그 때 완전히 메워지는 수평선의 개수가 Y개라면, Y를 최대로 만드는 X와 그 때의 Y를 하나의 공백을 사이에 두고 출력해야 한다.

만약 어떤 자리에 두어도 수평선을 하나도 메울 수 없거나 게임오버가 일어나는 경우라면 X와 Y를 둘다 0으로 출력한다.(게임오버는 새로 내려온 작대기가 맵상을 벗어난 경우에 일어난다. 새로나온 작대기가 맵의 가장자리에 걸쳐있는 경우는 게임오버가 아니다.)

### **예제 입력**

```
6 7
0 0 0 0 0 0
0 0 0 0 0 0
1 1 1 0 0 1
1 1 1 0 0 1
1 1 1 0 1 1
1 1 1 0 1 1
1 1 1 0 1 1

```

### **예제 출력**

```
4 3
```

## 📍코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main{
    static int[][] arr;
    static int C, R;
    static int[] position;
    public static void main(String[] args) throws IOException {
        // Please Enter Your Code Here
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());
        C = Integer.parseInt(st.nextToken());
        R = Integer.parseInt(st.nextToken());
        arr = new int[R][C];

        //입력받기
        for(int i=0; i<R; i++){
            st = new StringTokenizer(br.readLine());
            for(int j=0; j<C; j++){
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        checkPos();

        int[] result = new int[C];
        for(int i=0; i<C; i++){
            int x = position[i];
            if(x>0){
                //(1)테트리미노 채우기
                for(int j=0; j<4; j++) arr[x-j][i] = 1;
                //(2)수평선 검사
                result[i] = checkHor();
                //(3)테트리미노 삭제
                for(int j=0; j<4; j++) arr[x-j][i] = 0;
            }
        }
        int max = 0;
        int location = 0;
        for(int i=0; i<C; i++){
            if(max < result[i]){
                location = i;
                max = result[i];
            }
        }
        System.out.println((location+1) + " " + max);
    }
    /**
     * 테트리미노를 놓을 수 있는 위치 판단하는 코드
     * - 가장 위에서부터 막대기가 내려오기 때문에 위에서부터 0인 갯수를 카운트
     * - 카운드한 갯수가 테트리미노의 사이즈(4)보다 클 경우 놓을 수 있다
     * - position[4] = 7 -> (7, 4) 부터 막대기를 채울 수 있다는 의미
     */
    public static void checkPos(){
        position = new int[C];
        for(int i=0; i<C; i++){
            int cnt = 0;
            int x = 0; //테트리미노를 놓을 수 있는 행
            for(int j=0; j<R; j++){
                if(arr[j][i] == 0) {
                    cnt++;
                    x = j;
                }
                if(arr[j][i] == 1) break;
            }
            if(cnt >= 4) {
                position[i] = x;
            }
        }
    }
    public static int checkHor() {
        int line = 0;
        for(int i=0; i<R; i++){
            int rowCnt = 0;
            for(int j=0; j<C; j++){
                if(arr[i][j] == 1) rowCnt++;
            }
            if(rowCnt == C) line++;
        }
        return line;
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
        StringTokenizer st = new StringTokenizer(br.readLine());
        int C = Integer.parseInt(st.nextToken());
        int R = Integer.parseInt(st.nextToken());
        int[][] arr = new int[R+1][C+1];
        //입력받기
        for(int i=1; i<=R; i++){
            st = new StringTokenizer(br.readLine());
            for(int j=1; j<=C; j++){
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        /**
         * 테트리미노를 놓을 수 있는 위치 판단하는 코드
         * - 가장 위에서부터 막대기가 내려오기 때문에 위에서부터 0인 갯수를 카운트
         * - 카운드한 갯수가 테트리미노의 사이즈(4)보다 클 경우 놓을 수 있다
         * - position[4] = 7 -> (7, 4) 부터 막대기를 채울 수 있다는 의미
         */
        int[] position = new int[C+1];
        for(int i=1; i<=C; i++){
            int cnt = 0;
            int x = 0; //테트리미노를 놓을 수 있는 행
            for(int j=1; j<=R; j++){
                if(arr[j][i] == 0) {
                    cnt++;
                    x = j;
                }
                if(arr[j][i] == 1) break;
            }
            if(cnt >= 4) {
                position[i] = x;
            }
        }

        int[] result = new int[C+1];
        for(int i=1; i<=C; i++){
            int x = position[i];
            if(x>0){
                //(1)테트리미노 채우기
                for(int j=0; j<4; j++) arr[x-j][i] = 1;
                //(2)수평선 검사
                int line = 0;
                for(int k=1; k<=R; k++){
                    int rowCnt = 0;
                    for(int j=1; j<=C; j++){
                        if(arr[k][j] == 1) rowCnt++;
                    }
                    if(rowCnt == C) line++;
                }
                result[i] = line;
                //(3)테트리미노 삭제
                for(int j=0; j<4; j++) arr[x-j][i] = 0;
            }
        }
        int max = 0;
        int location = 0;
        for(int i=1; i<=C; i++){
            if(max < result[i]){
                location = i;
                max = result[i];
            }
        }
        System.out.println(location + " " + max);
    }
}
```

## 📍기록

- 생각보다 어렵고, 고려야할게 많았던 문제
- (1) 테트리미노가 들어갈 수 있는 자리 확인하기
- (2) 테트리미노를 넣었을때 몇개의 행이 사라지는지 삽입>확인>다시 삭제하기 (복구필요)

참고한 사이트
