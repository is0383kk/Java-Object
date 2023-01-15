# 第1章：クラス・インスタンス  
オブジェクト指向とはオブジェクトを中心に考えるシステムの構築方法の１つである。  
オブジェクト指向では実世界上の概念をオブジェクトという単位でシステム上に再現する。  

# クラスとインスタンス
オブジェクトを利用するときには、オブジェクトの設計図「クラス」を作成する。  
そして、クラス内でオブジェクトが持つ属性と操作を定義する。  
この「クラス」から生成されたオブジェクトを「インスタンス」と呼ぶ。  

- クラス：オブジェクトの定義
    - クラス名、属性、操作で構成される
    - 属性：データ(クラス内で定義された変
    - 操作：属性の値を使って行われる処理(クラス内で定義されたメソッド)

- インスタンス(≒オブジェクト)：クラスから生成されたオブジェクト  
    - クラスで定義されている属性(データ)に値を代入したもの  

- メッセージ：オブジェクトに送られる作業依頼
    - メッセージパッシング：あるオブジェクトから別のオブジェクトにメッセージを送ること
    
## Javaによるクラスの定義  
ここでは、Javaを使って、インスタンスの基となるクラスの作成方法を学ぶ。  
今回は「Employee.java」という名前でEmployeeクラスを作成する。  

- Employee.java
    - 属性：クラス内にフィールドを定義する
        - フィールド：属性を表す変数（employeeIdなど）
        ```java
        class Employee{
            // フィールド
            int employeeId;    // 社員番号
            String name;        // 氏名
            int salary;        // 基本給
            double multiplier; // ボーナスの基準月数
        }
        ```
    - 操作：メソッドで表現される
        ```java
        // メソッド
        void work(){
            System.out.println(name + "は働きました");
            // フィールドで定義した属性を使える
        }
        int calcSalary(){
            return salary;
        }
        ```
```java

public class Employee {
	// フィールド
	int employeeId;    // 社員番号
	String name;        // 氏名
	int salary;        // 基本給
	double multiplier; // ボーナスの基準月数

	// メソッド
	void work(){
	System.out.println(name + "は働きました");
	// フィールドで定義した属性を使える
	}
	
	int calcSalary(){
	return salary;
	}
}
```
## インスタンスの生成を行う
クラスを定義するだけでは、プログラムは動作しない。  
プログラムを動作させるには、クラスを基にインスタンスを制し絵する必要がある。これをインスタンス化と呼ぶ。  
  
今回はEmployeeクラスのインスタンスを作成する。  
インスタンスを生成するには「main」メソッドを持つ別のクラスを定義する。  

- Company.java：Employeeクラスのインスタンスを作成する
    - 実行すると「nullは働きました」と表示される

```java

public class Company {

	public static void main(String[] args) {
		// インスタンスの生成
		Employee taro = new Employee();
		taro.work();
	}
}
```
上記のようにフィールドに値が入っていない場合、フィールドにはデフォルト値が格納される  

|型|デフォルト値|
|---|---|
|数値型|0|
|boolean型|false|
|char型|'\u0000'|
|参照型|null|





# インスタンスを生成し値を代入する
前章の例のように、インスタンスを生成するだけでは何も起きない。  
そこで本章では、インスタンを利用するために以下の３つを学ぶ。
- インスタンスメンバの利用
- コンストラクタを利用してフィールド初期値を与える
- thisを使ってインスタンス内でフィールド・メソッドを利用する

## インスタンスメンバの利用
まずは、フィールドに値を代入する。  
以下のように「インスタンス変数.フィールド名」とするとフィールドの値を取り出すことができる
```java
public class Company {

	public static void main(String[] args) {
		// インスタンスの生成
		Employee yamada = new Employee();
		System.out.println("yamada.name : " + yamada.name);
		yamada.name = "山田";
		System.out.println("yamada.name : " + yamada.name);

	}

}
```
実行結果は以下のようになる  
一行目では初期値として代入された「null」が出力され、二行目ではフィールドに代入された「山田」が出力される  
```
yamada.name : null
yamada.name : 山田
```
  
---

次にメソッドを利用する。  
以下のように「インスタンス変数.メソッド名」とするとメソッドを呼び出すことができる。
```java
public class Company {

	public static void main(String[] args) {
		// インスタンスの生成
		Employee yamada = new Employee();
		yamada.name = "山田";
		
		yamada.work();
		yamada.salary = 190000;
		System.out.println("yamada.calcSalary : " + yamada.calcSalary());

	}

}
```
実行結果は以下のようになる  
```
山田は働きました
yamada.calcSalary : 190000
```

## コンストラクタを利用してフィールド初期値を与える
Javaではインスタンス生成時に指定した値えフィールドを初期化できる。  
これは、「コンストラクタ」と呼ばれるインスタンス生成時に呼び出される特別なメソッドにより行われている。

- コンストラクタ
    - メソッド名はクラス名と同じ
    - 戻り値の型は指定できない
    - インスタンス生成時にのみ呼び出される

Employee.javaにコンストラクタを追加する
- Employee.java
    - コンストラクタ
        - employeeId・name・salaryに初期値を代入するためのコンストラクタ
        ```java
        // コンストラクタ
        Employee(int Id, String na, int sal){
            employeeId = Id;
            name = na;
            salary = sal;
        }
        ```     
```java
public class Employee {
	// フィールド
	int employeeId;    // 社員番号
	String name;        // 氏名
	int salary;        // 基本給

	// コンストラクタ
	Employee(int id, String na, int sal){
		employeeId = id;
		name = na;
		salary = sal;
	}

	// メソッド
	void work(){
	System.out.println(name + "は働きました");
	// フィールドで定義した属性を使える
	}
	int calcSalary(){
	return salary;
	}
}
```
それでは、コンストラクタを利用してフィールドに初期値を代入してインスタンスを生成する
```java
public class Constructor {

	public static void main(String[] args) {
		// TODO 自動生成されたメソッド・スタブ
		Employee yamada = new Employee(200, "山田", 190000);
		System.out.println("yamada.name : " + yamada.name);
	}

}
```
実行結果は以下のようになり、コンストラクタを使ってフィールドに初期化を与えることができた
```
yamada.name : 山田
```
  
### デフォルトコンストラクタ
一方で引数のあるコンストラクタを定義すると「new Employee()」がコンパイルエラーとなってしまう。  
そこで、 <strong>引数のあるコンストラクタを定義する際は、引数のない「デフォルトコンストラクタ」を作成する必要がある。</strong>  
<strong>※コンストラクタが１つも無いと、引数のないデフォルトコンストラクタがインスタンス生成時に呼び出される。</strong>

- Employee.java
	- デフォルトコンストラクタのオーバロード

```java
public class Employee {
	// フィールド
	int employeeId;    // 社員番号
	String name;        // 氏名
	int salary;        // 基本給

	// デフォルトコンストラクタ
	Employee() {}

	// コンストラクタ
	Employee(int id, String na, int sal){
		employeeId = id;
		name = na;
		salary = sal;
	}

	// メソッド
	void work(){
	System.out.println(name + "は働きました");
	// フィールドで定義した属性を使える
	}
	int calcSalary(){
	return salary;
	}
}

```

## thisを使ってインスタンス内でフィールドを初期化する
以下のようにコンストラクタの引数名をフィールドにし、生成したインスタンスの値を表示すると指定した値で初期化できないという問題がある。  
```java
public class Employee {
	// フィールド
	int employeeId;    // 社員番号
	String name;        // 氏名
	int salary;        // 基本給

	// デフォルトコンストラクタ
	Employee() {}

	// コンストラクタ
	Employee(int employeeId, String name, int salary){
		employeeId = employeeId;
		name = name;
		salary = salary;
	}

}

```
```java
public class Constructor {

	public static void main(String[] args) {
		// TODO 自動生成されたメソッド・スタブ
		Employee yamada = new Employee(200, "山田", 190000);
		System.out.println("yamada.name : " + yamada.name);
		System.out.println("yamada.employeeId : " + yamada.employeeId);
		System.out.println("yamada.name : " + yamada.salary);
	}

}
```
実行結果は以下のようになり、インスタンスの中身が適切に初期化されない。  
```
yamada.name : null
yamada.employeeId : 0
yamada.name : 0

```

---

こうした問題を解決するために「this」というキーワードが用意されている。  
上記のクラスのコンストラクタに「this.フィールド名」と指定する。  
  
- Employee.java
	- 引数ありコンストラクタに「this」を用いる
	- 「this」を付けることでその変数がフィールドであることを示す  

```java
public class Employee {
	// フィールド
    int employeeId;    // 社員番号
    String name;        // 氏名
    int salary;        // 基本給
    
    // デフォルトコンストラクタ
    Employee() {}

    // コンストラクタ
    Employee(int employeeId, String name, int salary){
    	this.employeeId = employeeId;
    	this.name = name;
    	this.salary = salary;
    }

}
```
```java
public class Constructor {

	public static void main(String[] args) {
		// TODO 自動生成されたメソッド・スタブ
		Employee yamada = new Employee(200, "山田", 190000);
		System.out.println("yamada.name : " + yamada.name);
		System.out.println("yamada.employeeId : " + yamada.employeeId);
		System.out.println("yamada.name : " + yamada.salary);
	}

}
```
実行結果は以下のようになり、「this」を使うことで適切にインスタンスの値を初期化できていることがわかる
```
yamada.name : 山田
yamada.employeeId : 200
yamada.name : 190000
```
## thisを使って定義済みコンストラクタを呼び出す
複数のコンストラクタを定義した際、それぞれのコンストラクタで同じ処理を行う場合がある。  
この場合、「this()」を使うことでコンストラクタ内から別のコンストラクタを呼び出すことができる。  
  
- Employee.java：「this()」を使って別のコンストラクタを呼び出す
```java

public class Employee {
	// フィールド
    int employeeId;    // 社員番号
    String name;        // 氏名
    int salary;        // 基本給
    
    // デフォルトコンストラクタ
    Employee() {}

    // デフォルトコンストラクタ
    Employee() {}

    // コンストラクタ
    Employee(int employeeId){
    	this();
    	this.employeeId = employeeId;
    }
    
    Employee(int employeeId, String name, int salary){
    	this(employeeId);
    	this.name = name;
    	this.salary = salary;
    }

 }
```
<strong>※「this()」はコンストラクタ内の先頭行に付ける</strong>
<strong>※１つのコンストラクタに複数の「this()」は呼び出すことができない</strong>
<strong>※呼び出すコンストラクタの引数に合わせて形を変える。「Employee(int hoge)」の場合、「this(hoge)」とする。</strong>















## 静的メンバ  
- 静的メンバ：クラス内で共有したいフィールド値にstaticをつける  
    - 同一クラスで生成されたインスタンスで共有される  
    - クラス名.クラス変数
    - クラスメソッド(static ~())内でフィールド変数は扱えない(this.変数など)
- **インスタンスを生成していない際に、クラス内の変数やメソッドにアクセスしたい場合に使用**

```java
class Person{
    // フィールド
    String name;        // 氏名
    static int population=0; // 人口（インスタンス生成された回数）

    // コンストラクタ
    Person(){
        this.name = "未登録";
        Person.population++; // インスタンス生成時に1加算
    }

    // コンストラクタ
    Person(String name){
        this(); // population++を引き継ぐ
        this.name = name;
    }

    // メソッド
    void printName(){
        System.out.println(this.name); 
    }

    // スタティックメソッド(インスタンス未生成時にmainメソッドから呼び出し参照できる)
    static int getPopulation(){
        return Person.population; // スタティック変数へのアクセス(クラス名.変数)
    }
}
```

# パッケージとJava API  

##  パッケージとCLASSPATH  
- パッケージ：クラスを整理する仕組み
    - package パッケージ名;
    - import パッケージ名.クラス名;
    - パッケージ名の命名規則：jp.co.example（ドメインの逆順）
- CLASSPATH：クラス・パッケージを探す場所を指定  
    - CLATHPATH=フォルダパス1;フォルダパス2;

---

### package使用例
Employeeクラスを「app.staff」パッケージ内にある場合  
```java
package app.staff;
// workspace/app.staff/Employee.java
public class Employee{

}
```
  
異なるパッケージのクラスを利用する際は以下のように記述  
```java
class Company{
    public static void main (String[] args){
        app.staff.Employee Yamada = new app.staff.Employee();
    }
}
```

### インポート使用例
importを使用するとクラス名のみでインスタンス生成ができる  
```java
import app.staff.Employee;
class Company{
    public static void main (String[] args){
        Employee Yamada = new Employee();
    }
}
```
