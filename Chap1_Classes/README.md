# 第1章：クラス  

- クラス：オブジェクトの定義
    - クラス名、属性、操作で構成される
    - 属性：データ(クラス内で定義された変
    - 操作：属性の値を使って行われる処理(クラス内で定義されたメソッド)

- インスタンス(≒オブジェクト)：クラスから生成されたオブジェクト  
    - クラスで定義されている属性(データ)に値を代入したもの  

```java
class Employee{
    // フィールド
    int employeeID;    // 社員番号
    String name        // 氏名
    int salary;        // 基本給
    double multiplier; // ボーナスの基準月数

    // コンストラクタ
    Employee(int id. String na, int sal, double mu){
        employeeID = id;
        name = na;
        salaly = sal;
        multiplier = mu;
    }
    // コンストラクタ
    Employee(){} // 引数のないコンストラクタ（オーバロード）

    // メソッド
    void work(){
        System.out.println(name + "は働きました")
        // フィールドで定義した属性を使える
    }
    void calcSalary(){
        return salary
    }
}
```

## インスタンスの生成  
```java
class Company{
    public static void main(String[] args){
        // 引数の無いコンストラクタでインスタンスの作成
        Employee Yamada = new Employee() // インスタンス化
        // クラス名:Employee
        // 変数名:taro
        // コンストラクタ（クラス名と同じ）
        // フィールドの利用
        taro.name = "山田";
        System.out.println(name);

        // メソッドの利用
        taro.work();
        int answer = taro.calcSalary();

        // 引数のあるコンストラクタでインスタンスの作成
        Employee Yoshida = new Employee(200, "吉田", 40000, 2.0) // インスタンス化
    }    
}
```
- フィールドのデフォルト値  
    - 数値型は0
    - boolean型はfalse
    - char型は'\u0000'
    - 参照型はnull 

## コンストラクタ
- コンストラクタ:インスタンス生成時に実行される特別なメソッド  
    - **フィールドの初期化**
    - 名前はクラス名と同じ
    - 戻り値は指定できない 

## thisとthis()
- this:コンストラクタ作成の際、フィールド変数をそのまま使いたいときに便利  
    - this.フィールド変数名  
- this()：コンストラクタで定義された属性値をコンストラクタに持ってくることができる  
    - this()
    - this(引数1,引数2):引数のあるコンストラクタも呼べる

```java
class Employee{
    // フィールド
    int employeeID;    // 社員番号
    String name        // 氏名
    int salary;        // 基本給
    double multiplier; // ボーナスの基準月数

    // コンストラクタ
    Employee(){
        this.employeeID = 12345;
        this.name = "未登録";
        this.salaly = 330000;
        this.multiplier = 200000;
    }

    // コンストラクタ
    Employee(int id. String na, int sal, double mu){
        this.employeeID = EmployeeID;
        this.name = name;
        this.salaly = salaly;
        this.multiplier = multiplier;
    }

        // コンストラクタ
    Employee(int employeeId. String name){
        this(); // 引数のないコンストラクタの属性値がコピーされる

        // 追加で変更したい部分だけ変更  
        this.employeeID = employeeID; 
        this.name = name;
    }

    // メソッド
    void work(){
        System.out.println(name + "は働きました")
        // フィールドで定義した属性を使える
    }
    void calcSalary(){
        return salary
    }
}
```

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
