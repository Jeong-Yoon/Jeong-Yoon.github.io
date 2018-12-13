---
title: "Collections.sort()"
date: 2018-12-13 -0400
categories: 

---

<h1 id="collections.sort-예제">Collections.sort() 예제</h1>
<p><strong>Student1</strong></p>
<pre><code>ublic class Student1 implements Comparable&lt;Student1&gt;{  
    private String name;  
 private int kor;  
 private int eng;  
 private int math;  
  
 public Student1(String name, int kor, int eng, int math) {  
        this.name = name;  
 this.kor = kor;  
 this.eng = eng;  
 this.math = math;  
  }  
  
    public Student1() {  
    }  
  
    public String getName() {  
        return name;  
  }  
  
    public void setName(String name) {  
        this.name = name;  
  }  
  
    public int getKor() {  
        return kor;  
  }  
  
    public void setKor(int kor) {  
        this.kor = kor;  
  }  
  
    public int getEng() {  
        return eng;  
  }  
  
    public void setEng(int eng) {  
        this.eng = eng;  
  }  
  
    public int getMath() {  
        return math;  
  }  
  
    public void setMath(int math) {  
        this.math = math;  
  }  
  
    @Override  
  public boolean equals(Object o) {  
        if (this == o) return true;  
 if (o == null || getClass() != o.getClass()) return false;  
  
  Student1 student1 = (Student1) o;  
  
 if (kor != student1.kor) return false;  
 if (eng != student1.eng) return false;  
 if (math != student1.math) return false;  
 return name != null ? name.equals(student1.name) : student1.name == null;  
  }  
  
    @Override  
  public int hashCode() {  
        int result = name != null ? name.hashCode() : 0;  
  result = 31 * result + kor;  
  result = 31 * result + eng;  
  result = 31 * result + math;  
 return result;  
  }  
  
    @Override  
  public String toString() {  
        return "Student1{" +  
                "name='" + name + '\'' +  
                ", kor=" + kor +  
                ", eng=" + eng +  
                ", math=" + math +  
                '}';  
  }  
  
    @Override  
  public int compareTo(Student1 o) {  
        return name.compareTo(o.name);  
  }  
}
</code></pre>
<p><strong>StudentExam1</strong></p>
<pre><code>import java.util.ArrayList;  
import java.util.Collections;  
import java.util.Comparator;  
import java.util.List;  
  
public class StudentExam1 {  
    public static void main(String args[]) {  
        Student1 s1 = new Student1("Kim", 70, 60, 80);  
  Student1 s2 = new Student1("Jang", 85, 55, 90);  
  Student1 s3 = new Student1("Lee", 80, 50, 70);  
  
  List&lt;Student1&gt; slist = new ArrayList&lt;&gt;();  
  slist.add(s1);  
  slist.add(s2);  
  slist.add(s3);  
  
  System.out.println("*insert");  
 for (Student1 student : slist) {  
            System.out.println(student);  
  }  
        System.out.println();  
  
  System.out.println("*Name");  
  Collections.sort(slist);  
 for (Student1 student : slist) {  
            System.out.println(student);  
  }  
        System.out.println();  
  
  System.out.println("*Kor");  
  Collections.sort(slist, new NewStudentKoreanComparator());  
 for (Student1 student : slist) {  
            System.out.println(student);  
  }  
        System.out.println();  
  
  System.out.println("*Eng");  
  Collections.sort(slist,new NewStudentEnglishComparator());  
 for (Student1 student : slist) {  
            System.out.println(student);  
  }  
        System.out.println();  
  
  System.out.println("*Math");  
  Collections.sort(slist,new NewStudentMathComparator());  
 for (Student1 student : slist) {  
            System.out.println(student);  
  }  
  
    }  
}  
  
class NewStudentKoreanComparator implements Comparator&lt;Student1&gt; {  
    @Override  
  public int compare(Student1 o1, Student1 o2) {  
        return o1.getKor() - o2.getKor();  
  }  
}  
  
class NewStudentEnglishComparator implements Comparator&lt;Student1&gt; {  
    @Override  
  public int compare(Student1 o1, Student1 o2) {  
        return o1.getEng() - o2.getEng();  
  }  
}  
  
class NewStudentMathComparator implements Comparator&lt;Student1&gt; {  
    @Override  
  public int compare(Student1 o1, Student1 o2) {  
        return o1.getMath() - o2.getMath();  
  }  
}
</code></pre>
<ul>
<li>기본적으로 name을 기준으로 정렬하도록 Student1 클래스에는 compareTo 메소드를 오버라이딩</li>
<li>국어, 영어, 수학 점수로 정렬 할 수 있도록 하기 위해 클래스를 만들고 compare메소드를 오버라이딩.</li>
</ul>

