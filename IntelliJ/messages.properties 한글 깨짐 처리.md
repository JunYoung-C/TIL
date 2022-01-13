# messages.properties에서 한글이 ??로 표기되는 경우

## 1. File Encodings 설정

![image](https://user-images.githubusercontent.com/87891581/149347187-b5490fc3-6d68-4400-901e-a9941f51ea58.png)

- Global, Project, Properties Files의 Encoding을 모두 UTF-8로 바꾼다.
- Transperent native-to-ascii conversion를 체크한다.

## 2. application.properties에 다음 코드 추가

`spring.messages.encoding=UTF-8 `

## 3. Invalidate Caches 초기화

- File - Invalidate Caches - Reset
