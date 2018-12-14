---


---

<h1 id="윷놀이">윷놀이</h1>

<table>
<thead>
<tr>
<th>시간 제한</th>
<th>메모리 제한</th>
<th>제출</th>
<th>정답</th>
<th>정답 비율</th>
</tr>
</thead>
<tbody>
<tr>
<td>1초</td>
<td>128MB</td>
<td>-</td>
<td>-</td>
<td>-</td>
</tr>
</tbody>
</table><h2 id="문제">문제</h2>
<p>우리나라 고유의 윷놀이는 네 개의 윷짝을 던져서 배(0)와 등(1)이 나오는 숫자를 세어 도, 개, 걸, 윷, 모를 결정한다. 네 개 윷짝을 던져서 나온 각 윷짝의 배 혹은 등 정보가 주어질 때 도(배 한 개, 등 세 개), 개(배 두 개, 등 두 개), 걸(배 세 개, 등 한 개), 윷(배 네 개), 모(등 네 개) 중 어떤 것인지를 결정하는 프로그램을 작성하라.</p>
<h2 id="입력">입력</h2>
<p>첫째 줄부터 셋째 줄까지 각 줄에 각각 한 번 던진 윷짝들의 상태를 나타내는 네 개의 정수(0 또는 1)가 빈칸을 사이에 두고 주어진다.</p>
<h2 id="출력">출력</h2>
<p>첫째 줄부터 셋째 줄까지 한 줄에 하나씩 결과를 도는 A, 개는 B, 걸은 C, 윷은 D, 모는 E로 출력한다.</p>
<h2 id="예제-입력-1">예제 입력 1</h2>
<p>0 1 0 1<br>
1 1 1 0<br>
0 0 1 1</p>
<h2 id="예제-출력-1">예제 출력 1</h2>
<p>B<br>
A<br>
B</p>
<h2 id="출처">출처</h2>
<p>Olympiad &gt;  한국정보올림피아드시․도지역본선&gt;  지역본선 2009&gt;  초등부 1번</p>
<ul>
<li>잘못된 데이터를 찾은 사람:  djm03178</li>
<li>문제의 오타를 찾은 사람:  eric00513</li>
</ul>
<h2 id="알고리즘-분류">알고리즘 분류</h2>
<ul>
<li>구현</li>
</ul>
<pre><code>import java.util.Scanner;

public class Main {
   public static void main(String args[]) {
        Scanner sc = new Scanner(System.in);
        //int N = Integer.parseInt(sc.nextLine());
        String[] input = new String[3];
        int count = 0;
        for (int i = 0; i &lt; 3; i++) {
            input[i] = sc.nextLine();
            for (int j = 0; j &lt; input[i].length(); j++) {
                if (input[i].trim().charAt(j) == '0') {
                    count++;
                }
            }
            switch (count) {
                case 0:
                    System.out.println("E");
                    break;
                case 1:
                    System.out.println("A");
                    break;
                case 2:
                    System.out.println("B");
                    break;
                case 3:
                    System.out.println("C");
                    break;
                case 4:
                    System.out.println("D");
                    break;
            }
            count = 0;
        }
    }
}
</code></pre>

