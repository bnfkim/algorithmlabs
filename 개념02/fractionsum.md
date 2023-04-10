# ****fractionsum****

## 📍문제

### **입력**

---

첫째 줄과 둘째 줄에, 각 분수의 분자와 분모를 뜻하는 두 개의 자연수가 순서대로 주어진다. 입력되는 네 자연수는 모두 30,000 이하이다.

### **출력**

---

첫째 줄에 구하고자 하는 기약분수의 분자와 분모를 뜻하는 두 개의 자연수를 공백으로 구분하여 순서대로 출력한다.

### **예제 입력**

```
2 7
3 5

```

### **예제 출력**

```
31 35
```

## 📍코드

```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.StringTokenizer;

public class Main{
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

        StringTokenizer st = new StringTokenizer(br.readLine());
        int num = Integer.parseInt(st.nextToken());
        int deno = Integer.parseInt(st.nextToken());
        st = new StringTokenizer(br.readLine());
        int num2 = Integer.parseInt(st.nextToken());
        int deno2 = Integer.parseInt(st.nextToken());

        int numSum = num*deno2 + num2 * deno;
        int denoMul = deno*deno2;
        int gcd = gcd(numSum, denoMul);

        System.out.println(numSum/gcd + " " + denoMul/gcd);
    }

    public static int gcd(int a, int b){
        while(b!=0){
            int r = a%b;
            a = b;
            b = r;
        }
        return a;
    }
}
```

## 📍기록
