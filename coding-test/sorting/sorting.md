# 정렬

- 데이터를 특정한 기준에 따라서 순서대로 나열하는 것을 말한다.
- 아래 내용들은 오름차순 정렬을 수행하는 것을 전제로 되어있다.
- 코딩 테스트에서의 정렬 알고리즘 유형
    1. 정렬 라이브러리로 풀 수 있는 문제
    2. 정렬 알고리즘의 원리에 대해서 물어보는 문제 : 선택, 삽입, 퀵 등의 원리를 알아야 풀 수 있다.
    3. 더 빠른 정렬이 필요한 문제 : 계수 정렬 등의 다른 정렬 알고리즘을 이용하거나 문제에서 기존에 알려진 알고리즘의 구조적인 개선을 거쳐야 풀 수 있다.

## 인덱스

1. [선택 정렬](#선택-정렬)
2. [삽입 정렬](#삽입-정렬)
3. [버블 정렬](#버블-정렬)
4. [퀵 정렬](#퀵-정렬)
5. [계수 정렬](#계수-정렬)
6. [정렬 라이브러리](#정렬-라이브러리)

## 선택 정렬

- 알고리즘 원리
    1. 데이터가 무작위로 여러개 있다.
    2. 이중에서 가장 작은 데이터를 선택하고 맨 앞에 데이터와 바꾼다.
    3. 그 다음 작은 데이터를 선택해 앞에서 두 번째 데이터와 바꾸는 과정을 반복한다.
- 시간 복잡도 : O(N^2)

### 코드

```java
public class Main {
    void solution(int n, int[] arr) {
        for (int i = 0; i < n; i++) {
            int minIdx = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[minIdx] > arr[j]) {
                    minIdx = j;
                }
            }

            int tmp = arr[i];
            arr[i] = arr[minIdx];
            arr[minIdx] = tmp;
        }
    }

    public static void main(String[] args) {
        Main T = new Main();
        int n = 10;
        int[] arr = {7, 5, 9, 0, 3, 1, 6, 2, 4, 8};

        T.solution(n, arr);

        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

## 삽입 정렬

- 알고리즘 원리 : 데이터를 하나씩 확인하며, 각 데이터를 적절한 위치에 삽입한다.
- 데이터가 거의 정렬되어 있을 때 효율적으로 동작한다.
- 시간 복잡도 : O(N^2), 거의 정렬된 상태라면 N

### 코드

```java
public class Main {
    void solution(int n, int[] arr) {
        for (int i = 1; i < n; i++) { // 0번은 정렬이 되어있는 것으로 취급
            for (int j = i; j > 0; j--) {
                if (arr[j] < arr[j - 1]) {
                    int tmp = arr[j];
                    arr[j] = arr[j - 1];
                    arr[j - 1] = tmp;
                } else {
                    break;
                }
            }
        }
    }

    public static void main(String[] args) {
        Main T = new Main();
        int n = 10;
        int[] arr = {7, 5, 9, 0, 3, 1, 6, 2, 4, 8};

        T.solution(n, arr);

        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

## 버블 정렬

- 알고리즘 원리
    1. 이웃한 요소를 비교하고 교환하는 작업을 한바퀴 실행하면 첫 번째 요소가 정렬된다.
    2. 이를 총 n-1회 실행하면 배열이 정렬된다.### 코드
- 시간복잡도 : O(N^2)

### 코드

```java
public class Main {
    void solution(int n, int[] arr) {
        for (int i = 0; i < n - 1; i++) {
            for (int j = n - 1; j > i; j--) {
                if (a[j - 1] > a[j]) {
                    int tmp = arr[j];
                    arr[j] = arr[j - 1];
                    arr[j - 1] = tmp;
                }
            }
        }
    }

    public static void main(String[] args) {
        Main T = new Main();
        int n = 10;
        int[] arr = {7, 5, 9, 0, 3, 1, 6, 2, 4, 8};

        T.solution(n, arr);

        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

## 퀵 정렬

- 알고리즘 원리
    1. 피벗이라고 부르는 기준이 될 임의의 값을 선택한다.
    2. 피벗 이하의 그룹, 피벗 이상의 그룹으로 나눈다.
    3. 두 그룹에서 다시 각각의 피벗을 선정하고 그룹을 쪼갠다.
    4. 이를 반복하면 정렬된다.
- 정렬된 상태에 가까울 수록 최악의 시간 복잡도 O(N^2)를 가진다.
- 시간 복잡도 : O(N^2), 평균적으로 NlogN

### 코드

```java
public class Main {
    void solution(int n, int[] arr) {
        quickSort(0, n - 1, arr);
    }

    void quickSort(int start, int end, int[] arr) {
        if (start >= end) { // 원소가 1개인 경우 종료
            return;
        }
        int pivot = start; // 피벗은 첫번째 원소로 지정
        int lt = start + 1;
        int rt = end;

        while (lt <= rt) {
            // 피벗보다 큰 데이터 찾기, 오름차순이므로 왼쪽 구역에는 작은 값 몰어넣기
            while (lt <= end && arr[lt] <= arr[pivot]) {
                lt++;
            }
            while (rt > start && arr[rt] >= arr[pivot]) {
                rt--;
            }

            if (lt <= rt) {
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;
            } else { // 엇길린 경우 작은 데이터와 피벗 교체
                int temp = arr[pivot];
                arr[pivot] = arr[right];
                arr[right] = temp;
            }
        }

        quickSort(start, rt - 1, arr);
        quickSort(rt + 1, end, arr);
    }

    public static void main(String[] args) {
        Main T = new Main();
        int n = 10;
        int[] arr = {7, 5, 9, 0, 3, 1, 6, 2, 4, 8};

        T.solution(n, arr);

        for (int i : arr) {
            System.out.print(i + " ");
        }
    }
}
```

## 계수 정렬

- 데이터 크기가 제한되어 정수 형태로 표현할 수 있을 때망 사용할 수 있다.
- 일반적으로 가장 큰 데이터와 가장 작은 데이터의 차이가 1,000,000을 넘지 않을 때 효과적으로 사용 가능하다.
- 시간 복잡도 : O(N + K) - N은 데이터 개수, K는 최댓값
- 공간 복잡도 : O(N + K)

### 코드

```java
public class Main {
    int[] solution(int n, int max, int[] arr) {
        int[] cnt = new int[max + 1];

        for (int num : arr) {
            cnt[num] += 1;
        }

        return cnt;
    }

    public static void main(String[] args) {
        Main T = new Main();
        int n = 10;
        int[] arr = {7, 5, 9, 0, 3, 1, 6, 2, 4, 8};
        int max = Integer.MIN_VALUE;

        for (int num : arr) {
            if (max < i) {
                max = i;
            }
        }

        int[] cnt = T.solution(n, max, arr);

        for (int i = 0; i <= max; i++) {
            for (int j = 0; j < cnt[i]; j++) {
                System.out.print(i + " ");
            }
        }
    }
}
```

## 정렬 라이브러리

- 시간 복잡도 : O(NlogN)
- Arrays.sort() : 배열 정렬
- Collections.sort() : 리스트 정렬
- 단순 정렬시 오름차순 정렬
- 클래스 정렬시 정렬 방법
    1. 해당 클래스에 Comparable 인터페이스를 상속받아서 CompareTo 메서드를 구현한다.
    2. Comparator 인터페이스를 익명 클래스로 구현하여 sort 파라미터에 넘겨준다.  