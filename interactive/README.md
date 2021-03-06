# インタラクティブとアニメーション

## setupとdrawについて
<br>
processingでは、最初の一回だけ実行したい処理をsetup()内に、常時繰り返し実行したい処理をdraw()内に記述します。<br>
（サイズや背景設定などはsetup()内に、描画部分はdraw()に記述するのが流儀）<br><br>
<strong style="color:red;">drawは1秒間に60回実行されます。</strong>
<br><br>


### mouseを使った例
<br>
<img src="https://github.com/55Kaerukun/Processing/blob/master/images/intaraction_sample.png" width="800px">
<br>


### マウスの座標取得
mouseX (現在のマウスのx座標)<br>
mouseY (現在のマウスのY座標)<br>
```
// 例
ellipse(mouseX,mouseY,100, 100);
```

### 乱数の生成
random(256); 0以上、256未満の数　（0~255のいずれか）<br>
random(30,100); 30以上、100未満の数
```
// 例
fill(random(256),random(256),random(256));
```


```

void setup(){
  size(500,500);
  background(255);
}

void draw(){
  //background(255);
  fill(random(256),random(256),random(256));
  ellipse(mouseX, mouseY, 40,40);
  //ellipse(mouseX, mouseY, random(10,20),random(10,20));
}

// キーを押した時
void keyPressed() {
  // 白にする
  background(255,255,255);
}

```


<br>
<br>

# 変数
変数とは値をいれる箱のこと。C言語やJavaScript、ほぼ全てのプログラム言語で利用する重要概念。<br>
processing初級では、主に数字や真偽地(true, false)を入れたりするのに利用する。<br>

### 型 名前; 
#### int diameter;
### 代入(値を入れること); 
#### diameter = 200;
使用例: ellipse(250,250,diameter,diameter);<br><br>

diameter = 100;
のように、何度も上書きできる。<br>
<br>
<img src="https://github.com/55Kaerukun/Processing/blob/master/images/sample2-3.png" width="800px">
<br>
<br>

### 型の種類

<br>

型 | 内容
--- | ---
int | 整数
float | 少数
boolean | 真偽値
String | 文字列
PImage | 画像

<br>

# アニメーションの基礎
<br>
<br>
変数を使って、座標を少しずつ移動させてアニメーションを実現させる<br>

```
// 現在のposXの値に1ずつプラスする
posX = posX + 1;
```

<br>
<img src="https://github.com/55Kaerukun/Processing/blob/master/images/sample3.png" width="800px">
<br>

```
// ここで宣言
int posX;

void setup(){
  size(500,500);
  posX = 250;
}

void draw(){
  // 白で再度塗りつぶす
  background(255,255,255);
  fill(0,0,255);
  
  ellipse(posX,250,50,50);
  
  // x座標の更新
  posX = posX+1;
}
```


### if文で、画面右までに行ったら左に戻る

```

// ここで宣言
int posX;

void setup(){
  size(500,500);
  posX = 0;
}


void draw(){
  // 白で再度塗りつぶす
  background(255,255,255);
  fill(0,0,255);
  
  ellipse(posX,250,50,50);
  
  // x座標の更新
  posX = posX+1;
  
  /*
  if(posX > 500){
     posX = 0;
  }
  */
  
  if(posX > 550){
     posX = -50;
  }
  
}
```

<br>
問題！posYにして、上下運動に変更してみよう！<br><br>
問題！丸を二個にして、クロスするアニメーションを作ろう。

### 条件分岐(if文)は次回で詳しく！！
