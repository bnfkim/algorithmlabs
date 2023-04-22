## 📍문제

### **문제**

---

유니의 동네에는 오만원, 만원, 오천원, 천원, 오백원, 백원, 오십원, 십원 단위로 현금 출금이 가능한 특별한 ATM이 있다.

이 ATM은 출금할 금액을 입력하면 화폐 단위가 큰 돈부터 거슬러 준다. ATM 각 단위의 화폐 수는 무한하며 단점은 1원 단위의 돈은 출금해주지 않는다는 것이다.

각 단위의 돈이 몇 개가 출금되는지 출력하는 프로그램을 작성하시오.

### **입력**

---

첫째 줄에 테스트케이스의 수 T가 주어진다..

각 테스트케이스의 첫 줄에 유니가 출금할 금액 N이 주어진다. N은 10 이상, 100만 이하의 자연수로, 10의 배수다.

( 1 ≤ T ≤ 10 )

### **출력**

---

각 테스트케이스마다 '#'과 테스트케이스의 번호, 공백을 출력한 뒤 50,000원, 10,000원, 5,000원, 1,000원, 500원, 100원, 50원, 10원이 몇 개씩 출금되는지 순서대로 공백으로 구분하여 출력한다.

### **예제 입력**

```
5
971540
108170
994330
491370
532720

```

### **예제 출력**

```
#1
19 2 0 1 1 0 0 4
#2
2 0 1 3 0 1 1 2
#3
19 4 0 4 0 3 0 3
#4
9 4 0 1 0 3 1 2
#5
10 3 0 2 1 2 0 2
```

## 📍코드

```java
import java.util.Scanner;
public class Main{
    public static void main(String[] args){
        // Please Enter Your Code Here
        Scanner sc = new Scanner(System.in);
        int T = sc.nextInt();
        for(int t=1; t<=T; t++){
            int day = 1;
            int loveM = sc.nextInt();
            int loveD = sc.nextInt();
            int curM = sc.nextInt();
            int curD = sc.nextInt();
            int[] mons = new int[] {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31} ;

            if(curM == loveM) day += (curD - loveD);
            else {
                for(int i=loveM+1; i<curM; i++) day += mons[i];
                if (loveM > curM) { //일년이 지났을때
                    for(int i=loveM+1; i<13; i++) day += mons[i];
                    for(int i=1; i<curM; i++) day += mons[i];
                }
                day += (mons[loveM] - loveD + curD); //첫번째 달과 마지막 달 저장
            }
            System.out.println("#" + t + " " + day);
        }
    }
}
```

## 📍기록
