# ****division****

## 📍문제

### **문제**

---

임의의 자연수는 그보다 작은 자연수들의 합으로 표현될 수 있다. 예를 들어 4의 경우,

> 4= 3+1= 2+2= 2+1+1= 1+1+1+1
> 

위와 같은 방법으로 표현 될 수 있다. 이 때 , 숫자의 구성이 같으면서 그 순서만이 다른 경우는 같은 경우로 생각하는데, 예를 들어 다음 세 가지 경우는 모두 같은 경우이다.

> `2 + 1 + 1`, `1 + 2 + 1` , `1 + 1 + 2`
> 

자연수 n을 입력 받아 이를 n보다 작은 자연수들의 합으로 나타내는 방법을 모두 출력하는 프로그램을 재귀 호출을 사용하여 작성하시오.

### **입력**

---

첫 줄에 2 이상 20 이하의 자연수 n이 주어진다.

### **출력**

---

첫째 줄부터 모든 방법을 한 줄에 하나씩 출력한다. 하나의 식 안에는 큰 숫자가 앞으로 오도록 하고, 전체적으로는 앞의 숫자가 큰 식이 먼저 출력되도록 한다. 숫자와 더하기 사이에는 공백이 없다. 그리고 마지막 줄에는 나누어진 자연수의 개수를 출력한다.

### **예제 입력**

```
5

```

### **예제 출력**

```
4+1
3+2
3+1+1
2+2+1
2+1+1+1
1+1+1+1+1
6
```

## 📍코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main{
    private static final BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    private static final StringBuilder sb = new StringBuilder();
    static int count;
    static int[] result;
    public static void main(String[] args) throws IOException {
        /**
         * 두 정수 n, k를 입력받아 k개의 1을 가진 n자리 이진 패턴을 출력하는 프로그램을 작성
         */
        // Please Enter Your Code Here
        StringTokenizer st = new StringTokenizer(br.readLine());
        int n = Integer.parseInt(st.nextToken());
        result = new int[n];
        division(n, 0, 0);
        sb.append(count);
        System.out.print(sb);
    }

    public static void division(int n, int idx, int totalSum){
        //기저조건 : 모두 더한 숫자가 입력받은 숫자가 되면 종료
        if(totalSum == n) {
            sb.append(result[0]);
            for(int i=1; i<idx; i++){
                sb.append("+").append(result[i]);
            }
            count++;
            sb.append("\n");
        } else {
            int sum = 0;

            if (idx == 0) sum = n-1; //첫 인덱스일 경우
            else sum = n - totalSum;

            for(int i=sum; i>0; i--){
                //가장 큰 수 부터 배열 앞에 넣기
                result[idx] = i;
                //중복을 제거하기 위한 조건 (2+1+1 이 나와야하지 1+1+2 가 나와선 안 됨)
                if(idx>0 && result[idx] > result[idx-1]) continue;

                division(n, idx+1, totalSum+i);
            }
        }
    }
}
```

## 📍기록

- 중복을 제거하기 위한 조건이 필요
    - 큰 수부터 앞에다가 둘 것
    - 결과 배열 인덱스가 작은 값에, 결과 큰 값을 두기
- n = 입력받은 숫자, idx = 나뉘어진 갯수, totalSum = 현재까지 더해진 숫자
- 변하는 것 -> 나눌 갯수 & 나눌 갯수에 따라 나눠지는 숫자
- 나눌때, 큰 수부터 나눠야함 -> 배열위치+1, 나눌수-1
