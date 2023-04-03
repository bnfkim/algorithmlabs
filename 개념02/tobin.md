## 📍문제

### **문제**

---

두 정수 n, k를 입력받아 k개의 1을 가진 n자리 이진 패턴을 출력하는 프로그램을 작성하세요.

### **입력**

---

두 정수 n, k가 입력으로 주어진다. ( 0 < n <= 30, 0 <= k < 8 , n >= k )

### **출력**

---

결과를 내림차순으로 출력한다.

### **예제 입력**

```
2 1

```

### **예제 출력**

```
10
01

```

### **예제 입력**

```
2 0

```

### **예제 출력**

```
00

```

### **예제 입력**

```
4 2

```

### **예제 출력**

```
1100
1010
1001
0110
0101
0011

```

### **출처**

---

uwaterloo junior contest

## 📍코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main{
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final StringBuilder sb = new StringBuilder();
    static int n;
    static int[] arr;
    public static void main(String[] args) throws IOException {
        /**
         * 두 정수 n, k를 입력받아 k개의 1을 가진 n자리 이진 패턴을 출력하는 프로그램을 작성
         */
        // Please Enter Your Code Here
        StringTokenizer st = new StringTokenizer(br.readLine());
        n = Integer.parseInt(st.nextToken()); //자릿 수
        int k = Integer.parseInt(st.nextToken()); //1의 개수
        arr = new int[n]; //이진패턴을 표현할 배열
        printPattern(0, k);
        System.out.print(sb);
    }

    public static void printPattern(int x, int k){ //idx 번째 for문을 돌려야함
        //기저조건 : 더이상 출력할 1이 없으면 현재상태를 출력 후 종료함
        if(k==0) {
            for(int i=0; i<n; i++){
                sb.append(arr[i]);
            }
            sb.append("\n");
        } else {
            for(int i=x; i<n; i++){
                arr[i] = 1;
                printPattern(i+1, k-1);
                arr[i] = 0;
            }
        }
    }
}
```

## 📍기록

- 아이디어
    - n의 각 위치에서 1을 출력할 수 있는지 모두 검사하는 것
    - 여기서 각 위치는 1100에서 1,1,0,0이 각 위치가 됨
- 첫번째 자리 → 두번째 자리 → 세번째 자리 … N+1번째 자리 (N+1만큼 for문 실행)
- 함수 파라메터로 ‘자릿수(x), 1의 갯수(k)’ 를 넘겨줌
- 첫번째 자리에 1을 출력하고, 다시 재귀함수를 호출한다(N+1번째 for문 실행).
- 인자로 x+1, k-1을 넘겨준다 (x+1은 두번째 자리를 의미하고 k-1은 1을 출력할 수 있는 횟수)
- 항상 재귀함수가 시작되면 기저조건을 검사해준다
    - 만약 k==0이라면, 더이상 검사할 필요가 없다 → 현재 상태를 출력

- 참고 사이트

[[알고리즘 문제] Tobin](https://kosaf04pyh.tistory.com/72)
