# ****AI Finger Care****

## 📍문제

### **문제**

---

알고리즘랩스에는 직장동료를 누구보다 아끼는 개발팀 지니가 있다.

어느날 개발팀원들의 불꽃 코딩을 보고있던 지니는 팀원들의 손가락이 걱정되기 시작했다.

지니는 고민 끝에 팀원들의 손가락 피로도를 AI로 예측하여 마사지를 해주는 [인공지능 손가락 마사지기] 개발을 시작하려한다.

우선 손가락별 하루 코딩량을 측정하기 위해 아래와 같은 키보드를 모든 개발팀원들에게 지급하였다.

![https://storage.googleapis.com/instapage-thumbnails/thumbnail/20220705/1657008640-62047781-150x150-keyboard-1.jpg](https://storage.googleapis.com/instapage-thumbnails/thumbnail/20220705/1657008640-62047781-150x150-keyboard-1.jpg)

개발팀원 전원은 우수한 조기교육으로 독수리 타법을 사용하는 사람은 없다.

그래서 새끼손가락으로는 보라색, 약지로는 초록색, 중지로는 주황색, 왼손과 오른손 검지로는 각각 파란색과 빨간색을 누른다.

하루에 코딩할 내용이 입력으로 주어질 때, 지니를 도와 손가락별 타이핑 횟수를 출력하는 프로그램을 만드시오.

### **입력**

---

코딩할 내용이 n개의 문자로 구성되어 있는 문자열로 주어진다. 주어지는 문자열의 각 문자는 알파벳 소문자, 숫자 혹은 다음 문자열에 속한 특수문자 중 하나임이 보장된다. "-=[];',./" (1 <= n <= 1,000)

### **출력**

---

각 손가락이 타이핑하는 횟수를 여덟줄에 걸쳐 한 줄에 하나의 정수로 출력하시오.

출력순서 :

[왼손] 새끼손가락 > 약지 > 중지 > 검지 > [오른손] 검지 > 중지 > 약지 > 새끼손가락

### **예제 입력**

```
copyalgorithmlabs

```

### **예제 출력**

```
copy2 1 0 4 2 1 3 0

```

---

알고리즘랩스 알고리즘 경진대회(1회) / Regular Round 1

## 📍코드

```java
import java.util.Scanner;
public class Main{
    static String LP = "1qaz";
    static String LG = "2wsx";
    static String LY = "3edc";
    static String LB = "4rfv5tgb";
    static String RR = "6yhn7ujm";
    static String RY = "8ik,";
    static String RG = "9ol.";
    static String RP = "0p;/-['=]";
    static int[] cnt = new int[8];
    public static void main(String[] args){
        // Please Enter Your Code Here
        Scanner sc = new Scanner(System.in);
        String str = sc.next();
        for(int i=0; i<str.length(); i++){
            check(str.charAt(i));
        }
        for(int c : cnt) System.out.print(c + " ");
    }
    public static void check(char c){
        for(int i=0; i<LP.length(); i++){
            if(c == LP.charAt(i)) {
                cnt[0]++;
                return;
            }
        }
        for(int i=0; i<LG.length(); i++){
            if(c == LG.charAt(i)) {
                cnt[1]++;
                return;
            }
        }
        for(int i=0; i<LY.length(); i++){
            if(c == LY.charAt(i)) {
                cnt[2]++;
                return;
            }
        }
        for(int i=0; i<LB.length(); i++){
            if(c == LB.charAt(i)) {
                cnt[3]++;
                return;
            }
        }
        for(int i=0; i<RR.length(); i++){
            if(c == RR.charAt(i)) {
                cnt[4]++;
                return;
            }
        }
        for(int i=0; i<RY.length(); i++){
            if(c == RY.charAt(i)) {
                cnt[5]++;
                return;
            }
        }
        for(int i=0; i<RG.length(); i++){
            if(c == RG.charAt(i)) {
                cnt[6]++;
                return;
            }
        }
        for(int i=0; i<RP.length(); i++){
            if(c == RP.charAt(i)) {
                cnt[7]++;
                return;
            }
        }
    }

}
```

## 📍기록
