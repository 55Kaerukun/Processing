# 残像表現

アニメーションをリッチの見せる残像のテクニック<br>
毎フレーム更新する際に少し透明な四角をかぶせる<br><br>


<img src="https://github.com/55Kaerukun/Processing/blob/master/images/afterimage.png" width="500px">

```

// x座標
int posX;

void setup(){
  size(500,500);
  background(0);
  posX = 0;
}

void draw(){
  
  // 透明な四角を上から塗りつぶす
  fill(0,0,0,10);
  rect(0, 0, width, height);

  // 円の描画
  fill(0,0,255);
  ellipse(posX, height/2, 100, 100);
  
  // 座標の更新
  posX = posX+3;
  
  // 一番左に戻す
  if(posX > width){
    posX = 0;
  }
}

```
