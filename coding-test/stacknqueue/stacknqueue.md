# 스택과 큐

 [기본 원리](https://velog.io/@doforme/4.-%EC%8A%A4%ED%83%9D%EA%B3%BC-%ED%81%90)

## 코드

```java
public class Main {
    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();
        
        stack.push(1); // 데이터 삽입
        int n = stack.pop(); // 데이터 삭제
        stack.isEmpty(); // 스택이 비어있는지 확인
        
        Queue<Integer> que = new LinkedList<>();
        
        que.offer(1); // 데이터 삽입
        int n = que.poll(); // 데이터 삭제
        que.isEmpty(); // 큐가 비어있는지 확인
    }
}
```