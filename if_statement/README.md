# 条件分岐 （if文）

## バウンドする円
前回のアニメーションしていた円をバウンドさせてみましょう！<br>

<br>
<img src="https://github.com/55Kaerukun/Processing/blob/master/images/sample4..png" width="800px">
<br>

### 左右にバウンド
```

int posX;
int posY;
int speed;

void setup(){
  // 背景サイズ
  size(500,500);
  
  // 初位置
  posX = width/2;
  posY = height/2;
  
  // スピード
  speed = 3;
  
  noStroke();
}


void draw(){
  // 背景塗り潰し
  background(255,255,255);
  
  // 色設定
  fill(0,255,0);
 
  // 丸の位置移動
  posX = posX + speed;
  
  
  //壁にぶつかっていたら-1をかける
  if (posX > width || posX < 0) {
    speed = speed * -1;
  }
 
  //丸を書く
  ellipse(posX, posY, 50, 50);
  
}
```

### 上下左右にバウンド
変数sppdをもう一つY用に作るとずれる<br>
```
//グローバル変数
//x座標
int posX;
int posY;
int speedX;
int speedY;
int diameter; //円の直径

void setup(){
  size(500,500);
  background(255);
  posX = width/2;
  posY = height/2;
  speedX = 3;
  speedY = 6;
  diameter = 30;
}


void draw(){
  
  background(255);
  
  // 円の描画
  fill(0,255,0);
  ellipse(posX,posY,diameter,diameter);
  
  
  // 円の位置更新
  posX = posX + speedX;
  posY = posY + speedY;
  
  
  //posXのバウンド処理
  if(posX > width || posX < 0){
    speedX = speedX * -1;
  }
  
  //posYのバウンド処理
  if(posY > height || posY < 0){
    speedY = speedY * -1;
  }
  
}
```
<br>
<br>
<br>

# 配列

値を順序付けてたくさんしまえるローカールームのような存在。  
<img src="https://github.com/55Kaerukun/Processing/blob/master/images/array.jpg" width="500px">  
<br>


宣言方法 ↓ <br>
### 型[] 変数名 = new 型[個数]<br>
### float[] posX = new float[3]<br>

<br>
<img src="https://github.com/55Kaerukun/Processing/blob/master/images/array_ball.png" width="500px">
<br>

### 例: ランダムに3つのカラフルな円を描く
```
//円の個数
int NUM = 3;
// 円の座標
float[] posX = new float[NUM];
float[] posY = new float[NUM];
// 色相
float[] col = new float[NUM]; 

void setup(){
  size(500,500);
  colorMode(HSB,360,100,100,100);
  
  
  // X座標
  posX[0] = random(width);
  posX[1] = random(width);
  posX[2] = random(width);
  
  // Y座標
  posY[0] = random(height);
  posY[1] = random(height);
  posY[2] = random(height);
  
  // 色相
  col[0] = random(360);
  col[1] = random(360);
  col[2] = random(360);
  
  
}

void draw(){
  
  // 白
  background(360,0,100,100);
  
  fill(col[0],100,100,100);
  ellipse(posX[0],posY[0],100,100);
  fill(col[1],100,100,100);
  ellipse(posX[1],posY[1],50,50);
  fill(col[2],100,100,100);
  ellipse(posX[2],posY[2],70,70);
}


```
しかし、10個、100個となると記述が大変....

# for文

<br>
配列と相性がよく、一気に大量の処理が可能。
<br>
<br>

```

for (初期化式; 条件式; 変化式) {
    // 条件式がtrueのときに繰り返す処理
}

例: 変数NUMの数だけ、処理を繰り返す
int NUM = 4;

for(int i = 0; i < NUM; i++){
    println(i);
}

```


<br>
<img src="https://github.com/55Kaerukun/Processing/blob/master/images/bound_ball.png" width="500px">
<br>



```

//円の個数
int NUM = 100;

// 円の座標
float[] posX = new float[NUM];
float[] posY = new float[NUM];

//円の直径
float[] diameter = new float[NUM];

// 
float[] hue = new float[NUM];

void setup(){
  
  size(500,500);
  colorMode(HSB,360,100,100,100);
  
  for(int i = 0; i<NUM; i++){
    posX[i] = random(width);
    posY[i] = random(height);
    diameter[i] = random(10,50);
    hue[i] = random(360);
  }
}

void draw(){
  // 白
  background(360,0,100,100);
  for(int i = 0; i<NUM; i++){
    fill(hue[i],100,100,100);
    ellipse(posX[i],posY[i],diameter[i],diameter[i]);
  }
}

```

# バウンドのアニメーションを配列 + for文で大量表示させてみよう！

```

//グローバル変数
//円の個数
int NUM = 50;
//円座標
float[] posX = new float[NUM];
float[] posY = new float[NUM];
//スピード
float[] speedX = new float[NUM];
float[] speedY = new float[NUM];
//円の直径
float[] diameter = new float[NUM];
//色相
int[] hue = new int[NUM];

void setup(){
  size(500,500);
  noStroke();
  //初期値 配列にfor
  
  for(int i=0; i<NUM; i+=1){
    posX[i] = random(width);
    posY[i] = random(height);
    speedX[i] = random(-4,4);
    speedY[i] = random(-4,4);
    diameter[i] = random(4,20);
    hue[i] = (int)random(360);
  }
}


void draw(){
  background(0);
  colorMode(HSB,360,100,100,100);
  
  for(int i=0; i<NUM; i++){
    fill(hue[i],100,100,100);
    
    //XYの座標にスピードを足す
    posX[i] = posX[i] + speedX[i];
    posY[i] = posY[i] + speedY[i];
    //跳ね返り
    if(posX[i] > width || posX[i] <0){
      speedX[i] = speedX[i] * -1;
    }
    if(posY[i] > height || posY[i] <0){
      speedY[i] = speedY[i] * -1;
    }
    ellipse(posX[i],posY[i],diameter[i],diameter[i]);
  }
}

```
