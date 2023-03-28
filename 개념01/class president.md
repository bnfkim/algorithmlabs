# ****class president****

## 📍문제

### **문제**

---

오민식 선생님은 올해 형택초등학교 6학년 1반 담임을 맡게 되었다. 오민식 선생님은 우선 임시로 반장을 정하고 학생들이 서로 친숙해진 후에 정식으로 선거를 통해 반장을 선출하려고 한다. 그는 자기반 학생 중에서 1학년부터 5학년까지 지내오면서 한번이라도 같은 반이었던 사람이 가장 많은 학생을 임시 반장으로 정하려 한다.

그래서 오민식 선생님은 각 학생들이 1학년부터 5학년까지 몇 반에 속했었는지를 나타내는 표를 만들었다. 예를 들어 학생 수가 5명일 때의 표를 살펴보자.

![https://alms-problem.s3.ap-northeast-2.amazonaws.com/class_president.jpg](https://alms-problem.s3.ap-northeast-2.amazonaws.com/class_president.jpg)

위 경우에 4번 학생을 보면 3번 학생과 2학년 때 같은 반이었고, 3번 학생 및 5번 학생과 3학년 때 같은 반이었으며, 2번 학생과는 4학년 때 같은 반이었음을 알 수 있다. 그러므로 이 학급에서 4번 학생과 한번이라도 같은 반이었던 사람은 2번 학생, 3번 학생과 5번 학생으로 모두 3명이다. 이 예에서 4번 학생이 전체 학생 중에서 같은 반이었던 학생 수가 제일 많으므로 임시 반장이 된다.

각 학생들이 1학년부터 5학년까지 속했던 반이 주어질 때, 임시 반장을 정하는 프로그램을 작성하시오.

### **입력**

---

첫째 줄에는 반의 학생 수를 나타내는 정수가 주어진다. 학생 수는 3 이상 1000 이하이다. 둘째 줄부터는 1번 학생부터 차례대로 각 줄마다 1학년부터 5학년까지 몇 반에 속했었는지를 나타내는 5개의 정수가 빈칸 하나를 사이에 두고 주어진다. 주어지는 정수는 모두 1 이상 9 이하의 정수이다.

### **출력**

---

첫 줄에 임시 반장으로 정해진 학생의 번호를 출력한다. 단, 임시 반장이 될 수 있는 학생이 여러 명인 경우에는 그 중 가장 작은 번호만 출력한다.

### **예제 입력**

```
5
2 3 1 7 3
4 1 9 6 8
5 5 2 4 4
6 5 2 6 7
8 4 2 2 2

```

### **예제 출력**

```
4

```

### **출처**

---

한국정보올림피아드 KOI 2006 본선 초등부1번

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
        int n = Integer.parseInt(br.readLine());
        int[][] arr = new int[n+1][6];

        for(int i=1; i<=n; i++){
            StringTokenizer st = new StringTokenizer(br.readLine());
            for(int j=1; j<=5; j++){
                arr[i][j] = Integer.parseInt(st.nextToken());
            }
        }
        int result = 0;
        int resultNumber = 1;
        for(int i = 1; i<=n; i++) {
            int numStudent = 0;
            for(int j = 1; j<=n; j++) {
                if(i == j) continue;
                if(arr[i][1] == arr[j][1]
                        || arr[i][2] == arr[j][2]
                        || arr[i][3] == arr[j][3]
                        || arr[i][4] == arr[j][4]
                        || arr[i][5] == arr[j][5]) {
                    numStudent++;
                }
            }
            if(numStudent > result) {
                result = numStudent;
                resultNumber = i;
            }
        }
        System.out.println(resultNumber);
    }
}
```

## 📍기록

- **모든 학생이 같은반이 된 적이 없었을 경우 고려**
    - resultNumber 초기화를 1로 두기
