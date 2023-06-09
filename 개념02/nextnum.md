# nextnum

## 📍문제

### **문제**

---

위키피디아에 따르면 등차수열 AP는 연속되는 두 숫자의 차가 같은 숫자들이 연속되는 수열이다. 예를 들어, 수열 3,5,7,9,11,13…. 은 공차(연속된 숫자의 차이) 2를 가지는 등차수열이다. 이 문제에서 공차는 0이 아닌 정수이다.

등비수열 GP는 이전의 숫자에 0이 아닌 공비(연속된 숫자의 비율)를 곱하여 구하는 수열이다. 예를 들어 수열 2,6,18,54 는 공비가 3인 등비수열이다. 이 문제에서 공비는 0이 아닌 정수이다. 수열을 구성하는 세 개의 숫자가 주어졌을 때, 주어진 수열이 등차 수열인지 등비수열인지를 결정하고, 다음에 연속될 숫자를 결정하는 프로그램을 작성하시오.

### **입력**

---

입력은 여러 개의 테스트 케이스로 이루어져 있다.

- 각각의 케이스는 3개의 정수 a1, a2, a3가 한줄로 주어질 것이다. (−10, 000 < a1, a2, a3 < 10, 000)
- a1, a2, a3는 각각 다르다.
- 마지막 테스트 케이스는 세 개의 0으로 주어진다.

### **출력**

---

각 테스트케이스마다 한 줄씩 결과를 출력한다. 형태 : XX v (XX는 주어진 수열이 등차수열이면 ‘AP’ 이고 등비수열이면 ‘GP’이다. v는 수열 다음에 오는 상수이다. ) 모든 입력 케이스는 등비수열 또는 등차수열임이 보장되어 있다.

```
copyXX V

```

XX부분은 AP 또는 GP로 주어진 수들이 등차수열을 이룰 경우 AP를, 등비수열을 이룰 경우 GP를 출력한다. V는 주어진 수들 다음에 나올 수이다. 모든 입력은 항상 등차수열이나 등비수열이다.

### **예제 입력**

```
4 7 10
2 6 18
0 0 0

```

### **예제 출력**

```
AP 13
GP 54

```

### **출처**

---

2010 Arab Collegiate Programming Contest A번

## 📍코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main{
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        while(true) {
            StringTokenizer st = new StringTokenizer(br.readLine());
            int a = Integer.parseInt(st.nextToken());
            int b = Integer.parseInt(st.nextToken());
            int c = Integer.parseInt(st.nextToken());

            if(a==0 && b==0 && c==0) return;

            if ((a+c) == (b*2)) System.out.print("AP " + (c+b-a));
            else if ((a*c) == (b*b)) System.out.print("GP " + (c*b/a));
            System.out.println();
        }
    }
}
```

## 📍기록
