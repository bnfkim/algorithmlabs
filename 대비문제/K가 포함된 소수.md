# **K가 포함된 소수**

## 📍문제

### **문제**

---

정수론을 공부중인 유니와 지니는 서로에게 퀴즈를 낸다.

퀴즈는 세 자연수 v, s, e로 구성되는데, s 이상 e 이하의 자연수 중 v라는 숫자가 포함되어 있으면서 소수인 수가 몇 개인지 대답해야 한다. 여기서 v는 1 이상 9 이하의 자연수, s, e는 1 이상 1,000,000 이하의 자연수고 s보다 e가 크거나 같다. 정수론과 함께 프로그래밍을 배운 유니는 이 작업을 코드로 구현할 수 있다. 유니가 할 수 있으면 당신도 할 수 있다. 구현해보자.

### **입력**

---

첫째 줄에 테스트케이스의 수 T가 주어진다..

각 테스트케이스의 첫 줄에 v, s, e가 공백으로 구분되어 주어진다.

( 1 ≤ T ≤ 100 )

### **출력**

---

각 테스트케이스마다 '#'과 테스트케이스의 번호, 공백을 출력한 뒤 퀴즈의 정답을 출력한다.

### **예제 입력**

```
10
4 65 100
2 50 57
7 3 95
5 12 76
4 45 88
7 20 57
1 24 47
6 29 85
8 66 90
2 34 100

```

### **예제 출력**

```
#1 0
#2 0
#3 8
#4 2
#5 1
#6 2
#7 2
#8 2
#9 2
#10 0
```

## 📍코드

```java
import java.util.*;
public class Main{
    public static void main(String[] args)  {
        // Please Enter Your Code Here
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        for(int t=1; t<=T; t++){
            int cnt = 0;
            int v = sc.nextInt(); //포함될 숫자 1<=v<=9
            int s = sc.nextInt(); //시작수
            int e = sc.nextInt(); //끝 수
            //체를 이용해 소수 판별해놓기
            boolean[] isNotPrime = new boolean[e+1];
            isNotPrime[1] = true;
            for(int i=2; i<=e; i++){
                if(isNotPrime[i]) continue; //소수가 아니면 패스
                for(int j=i*2; j<=e; j+=i) isNotPrime[j] = true;
            }
            for (int i=s; i<=e; i++) {
                if(!isNotPrime[i]){
                    int tmp = i;
                    while(tmp>0){
                        if(tmp%10 == v) {
                            cnt++;
                            break;
                        }
                        tmp = tmp/10;
                    }
                }
            }
            System.out.println("#" + t + " " + cnt);
        }
    }
}
```

## 📍기록

- 처음에 테스트케이스 1개 틀림
    - why?) → `isNotPrime[1] = true;` 안 넣어놨었는데 이게 나중에 테스트 케이스에 걸림
