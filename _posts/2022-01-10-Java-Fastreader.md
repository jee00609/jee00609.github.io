---
title: "[Java] FastReader 메모"
categories:
  - Java
tags: 
  - Java
  - 
last_modified_at: 2022-01-10
---

학교 졸업 전 마지막으로 특강을 듣는 중이다.

내가 주로 사용하는 언어는 Java 와 Python 인데 코딩 테스트를 Python 으로만 준비했었다.

혹시 몰라서 Java 로 코딩 테스트 문제를 풀려고 생각했더니 효율성에서 좀 문제가 나는 것 같다.

이번 특강에서 아래와 같은 코드를 소개받았는데 코딩 테스트에서 매우 효율적일 것 같아 메모한다.

```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) {
        FastReader fr = new FastReader(); // 문제 해결 소스 코드
        int a = fr.nextInt();
        int b = fr.nextInt();
        System.out.println(a + b);
    }
    public static class FastReader {
        BufferedReader br;
        StringTokenizer st;
        public FastReader() { br = new BufferedReader(new InputStreamReader(System.in)); }
        public FastReader(String s) throws FileNotFoundException { br = new BufferedReader(new FileReader(new File(s))); }
        String next() {
            while (st == null || !st.hasMoreElements()) {
                try { st = new StringTokenizer(br.readLine()); }
                catch (IOException e) { e.printStackTrace(); }
            }
            return st.nextToken();
        }
        int nextInt() { return Integer.parseInt(next()); }
        long nextLong() { return Long.parseLong(next()); }
        double nextDouble() { return Double.parseDouble(next()); }
        String nextLine() {
            String str = "";
            try { str = br.readLine(); }
            catch (IOException e) { e.printStackTrace(); }
            return str;
        }
    }
}
```

## 참고 사이트
[동빈나 BOJ Java 코드](https://github.com/ndb796/BOJ_Java/blob/main/Main.java)