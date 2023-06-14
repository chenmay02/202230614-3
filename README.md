# 202230614-3

---
tags:2023大一下學期-期末作業
---
# 設計貓咪圖案
![](https://hackmd.io/_uploads/rJxnzBJU2.gif)
---
貓咪自己移動，並有線條及內顏色的分層
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

// class:類別
class Obj {  //宣告一個類別，針對一個畫的圖案
   constructor(){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
      this.p = {x:random(width),y:random(height)} // 物件的初始位置
      this.v = {x:random(-1,1),y:random(-1,1)} //物件的移動速度
      this.size = random(8,12) //物件的放大倍率(亂數抽8-12間)
      this.color = random(fill_colors)
      this.stroke = random(line_colors)
   }

   draw(){ //劃出物件形狀
    push() //執行push()後，依照設定，設定原點(0,0)的位置
      translate(this.p.x,this.p.y) //以該物件位置為原點
      scale(this.v.x<0?1:-1,-1)
      fill(this.color) 
      stroke(this.stroke)
      strokeWeight(4)//線條粗細
      beginShape()
      for(var k=0; k <points.length; k=k+1){
        // line(points[k][0]*this.size,points[k][1]*this.size,points[k+1][0]*this.size,points[k+1][1]*this.size) //需要提供2個點的座標
        // vertex(points[k][0]*this.size,points[k][1]*this.size) //只要設定一個點，當指令到endshape()，會把所有的點串接再一起
        curveVertex(points[k][0]*this.size,points[k][1]*this.size) //畫線為圓弧方式畫圖
      }
      endShape()
    pop() //執行pop()，原點(0,0)設定回到整個視窗的左上方
   }
   update(){
    this.p.x = this.p.x +this.v.x
    this.p.y = this.p.y +this.v.y
   }
}

var ball  //目前要處理的物件，暫時放在ball變數內
var balls =[] //產生的"所有"的物件
function setup() {
  createCanvas(windowWidth, windowHeight);
  for(var i=0;i<20;i=i+1){ // i=0,1,2,3,4,...19，i的數課可以任調
    ball = new Obj() //產生一個Obj class元件
    balls.push(ball) //把ball的物件放入到balls陣列內
  }
}


function draw() {
  background(220);
 for(var j=0;j<balls.length;j=j+1){
  ball =balls[j]
  ball.draw()
  ball.update()
 }
}
```
![](https://hackmd.io/_uploads/S1rBXrJ83.gif)
---
滑鼠按一下，就出現一個貓咪
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

// class:類別
class Obj {  //宣告一個類別，針對一個畫的圖案
   constructor(args){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
      this.p = args.p||{x:random(width),y:random(height)} // 物件的初始位置
      this.v = {x:random(-1,1),y:random(-1,1)} //物件的移動速度
      this.size = random(8,12) //物件的放大倍率(亂數抽8-12間)
      this.color = random(fill_colors) //充滿顏色
      this.stroke = random(line_colors) //外框線條顏色
   }
   draw(){ 
    push() //執行push()後，依照設定，設定原點(0,0)的位置
      translate(this.p.x,this.p.y) //以該物件位置為原點
      scale(this.v.x<0?1:-1,-1)    //X軸的放大倍率，如果this.v.x<0條件成立，值為1，否則為-1；Y軸的-1，為上下翻轉
      fill(this.color) 
      stroke(this.stroke)
      strokeWeight(4)//線條粗細
      beginShape()
      for(var k=0; k <points.length; k=k+1){
        // line(points[k][0]*this.size,points[k][1]*this.size,points[k+1][0]*this.size,points[k+1][1]*this.size) //需要提供2個點的座標
        // vertex(points[k][0]*this.size,points[k][1]*this.size) //只要設定一個點，當指令到endshape()，會把所有的點串接再一起
        curveVertex(points[k][0]*this.size,points[k][1]*this.size) //畫線為圓弧方式畫圖
      }
      endShape()
    pop() //執行pop()，原點(0,0)設定回到整個視窗的左上方
   }
   update(){ //移動的程式內容
    this.p.x = this.p.x +this.v.x
    this.p.y = this.p.y +this.v.y
   }
}

var ball  //"目前要處理"的物件，暫時放在ball變數內
var balls =[] //產生更多物件
function setup() {
  createCanvas(windowWidth, windowHeight);
  for(var i=0;i<35;i=i+1){ // i=0,1,...34，i的數課可以任調
    ball = new Obj({}) //產生一個Obj class元件
    balls.push(ball) //把ball的物件放入到balls陣列內
  }
}


function draw() {
  background(220);
//  for(var j=0;j<balls.length;j=j+1){
//   ball =balls[j]
//   ball.draw()
//   ball.update()
//  }
 for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
 {
   ball.draw()
   ball.update()
 }
}

// --------按一下，就產生一個貓咪-------------
function mousePressed(){
  ball = new Obj({
    p:{x:mouseX, y:mouseY}
  }) //在滑鼠按下的地方，產生一個新的Obj class元件
  balls.push(ball) //把ball的物件放入到balls陣列內
}
```
![](https://hackmd.io/_uploads/SJWfsry82.gif)
---
貓咪碰到邊界，彈回來
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

// class:類別
class Obj {  //宣告一個類別，針對一個畫的圖案
   constructor(args){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
      this.p = args.p||{x:random(width),y:random(height)} // 物件的初始位置
      this.v = {x:random(-1,1),y:random(-1,1)} //物件的移動速度
      this.size = random(8,12) //物件的放大倍率(亂數抽8-12間)
      this.color = random(fill_colors) //充滿顏色
      this.stroke = random(line_colors) //外框線條顏色
   }
   draw(){ 
    push() //執行push()後，依照設定，設定原點(0,0)的位置
      translate(this.p.x,this.p.y) //以該物件位置為原點
      scale(this.v.x<0?1:-1,-1)    //X軸的放大倍率，如果this.v.x<0條件成立，值為1，否則為-1；Y軸的-1，為上下翻轉
      fill(this.color) 
      stroke(this.stroke)
      strokeWeight(4)//線條粗細
      beginShape()
      for(var k=0; k <points.length; k=k+1){
        // line(points[k][0]*this.size,points[k][1]*this.size,points[k+1][0]*this.size,points[k+1][1]*this.size) //需要提供2個點的座標
        // vertex(points[k][0]*this.size,points[k][1]*this.size) //只要設定一個點，當指令到endshape()，會把所有的點串接再一起
        curveVertex(points[k][0]*this.size,points[k][1]*this.size) //畫線為圓弧方式畫圖
      }
      endShape()
    pop() //執行pop()，原點(0,0)設定回到整個視窗的左上方
   }
//++++++++++++++++貓咪碰到邊界彈回來++++++++++++++++++++++++++++++++++++++++
   update(){ //移動的程式內容
    this.p.x = this.p.x +this.v.x //x軸目前的位置(this.p.x)加上X軸移動速度(this.v.x)
    this.p.y = this.p.y +this.v.y //y軸目前的位置(this.p.y)加上y軸移動速度(this.v.y)
    if(this.p.x<=0 || this.p.x>=width){ //碰到X軸左邊(<=0)，或是碰到右邊(>=width)
      this.v.x = -this.v.x        //把速度方向改變
    }
    if(this.p.y<=0 || this.p.y>=height){ //碰到y軸上邊(<=0)，或是碰到下邊(>=height)
      this.v.y = -this.v.y        //把速度方向改變
    }
   }
}
//++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

var ball  //"目前要處理"的物件，暫時放在ball變數內
var balls =[] //產生更多物件
function setup() {
  createCanvas(windowWidth, windowHeight);
  for(var i=0;i<35;i=i+1){ // i=0,1,...34，i的數課可以任調
    ball = new Obj({}) //產生一個Obj class元件
    balls.push(ball) //把ball的物件放入到balls陣列內
  }
}


function draw() {
  background(220);
//  for(var j=0;j<balls.length;j=j+1){
//   ball =balls[j]
//   ball.draw()
//   ball.update()
//  }
 for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
 {
   ball.draw()
   ball.update()
 }
}

// --------按一下，就產生一個貓咪-------------
function mousePressed(){
  ball = new Obj({
    p:{x:mouseX, y:mouseY}
  }) //在滑鼠按下的地方，產生一個新的Obj class元件
  balls.push(ball) //把ball的物件放入到balls陣列內
}
```
![](https://hackmd.io/_uploads/HJ7-AByIh.gif)

---
在貓咪上按下滑鼠，貓咪消失/分數+1
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

// class:類別
class Obj {  //宣告一個類別，針對一個畫的圖案
   constructor(args){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
      this.p = args.p||{x:random(width),y:random(height)} // 物件的初始位置
      this.v = {x:random(-1,1),y:random(-1,1)} //物件的移動速度
      this.size = random(8,12) //物件的放大倍率(亂數抽8-12間)
      this.color = random(fill_colors) //充滿顏色
      this.stroke = random(line_colors) //外框線條顏色
   }
   draw(){
    push() //執行push()後，依照設定，設定原點(0,0)的位置
      translate(this.p.x,this.p.y) //以該物件位置為原點
      scale(this.v.x<0?1:-1,-1)    //X軸的放大倍率，如果this.v.x<0條件成立，值為1，否則為-1；Y軸的-1，為上下翻轉
      fill(this.color) 
      stroke(this.stroke)
      strokeWeight(4)//線條粗細
      beginShape()
      for(var k=0; k <points.length; k=k+1){
        // line(points[k][0]*this.size,points[k][1]*this.size,points[k+1][0]*this.size,points[k+1][1]*this.size) //需要提供2個點的座標
        // vertex(points[k][0]*this.size,points[k][1]*this.size) //只要設定一個點，當指令到endshape()，會把所有的點串接再一起
        curveVertex(points[k][0]*this.size,points[k][1]*this.size) //畫線為圓弧方式畫圖
      }
      endShape()
    pop() //執行pop()，原點(0,0)設定回到整個視窗的左上方
   }
   update(){ //移動的程式內容
    this.p.x = this.p.x +this.v.x //x軸目前的位置(this.p.x)加上X軸移動速度(this.v.x)
    this.p.y = this.p.y +this.v.y //y軸目前的位置(this.p.y)加上y軸移動速度(this.v.y)
    if(this.p.x<=0 || this.p.x>=width){ //碰到X軸左邊(<=0)，或是碰到右邊(>=width)
      this.v.x = -this.v.x        //把速度方向改變
    }
    if(this.p.y<=0 || this.p.y>=height){ //碰到y軸上邊(<=0)，或是碰到下邊(>=height)
      this.v.y = -this.v.y        //把速度方向改變
    }
   }
   isBallInRanger(){ //判斷滑鼠按下的位置，是否在物件範圍內
    let d = dist(mouseX,mouseY,this.p.x,this.p.y) //計算(mouseX,mouseY)和(this.p.x,this.p.y)兩點的距離
    if(d<4*this.size){
      return true   //滑鼠與物件的距離<物件寬度，代表碰觸了，傳回true值
    }else{
      return false  //滑鼠與物件的距離>物件寬度，代表沒有碰觸，傳回false值
    }
   }
}

var ball  //"目前要處理"的物件，暫時放在ball變數內
var balls =[] //產生更多物件
var score = 0
function setup() {
  createCanvas(windowWidth, windowHeight);
  for(var i=0;i<60;i=i+1){ // i=0,1,2,3,4,...59，i的數課可以任調
    ball = new Obj({}) //產生一個Obj class元件
    balls.push(ball) //把ball的物件放入到balls陣列內
  }
}


function draw() {
  background(220);
//  for(var j=0;j<balls.length;j=j+1){
//   ball =balls[j]
//   ball.draw()
//   ball.update()
//  }

 for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
 {
   ball.draw()
   ball.update()
 }
 textSize(50)
 text(score,50,50)//在座標(50,50)上，顯示score分數內容

}


function mousePressed(){

  //++++++++++產生一個物件+++++++++++++++++++++++++++++++++++
  // ball = new Obj({
  //   p:{x:mouseX, y:mouseY}
  // }) //在滑鼠按下的地方，產生一個新的Obj class元件
  // balls.push(ball) //把ball的物件放入到balls陣列內
  //+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

  
  //----------在物件上按下滑鼠，物件消失，分數+1---------------------------
  for(let ball of balls){ //檢查每一個物件
    if(ball.isBallInRanger()){ 
      balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
      score = score + 1
    }
  }
  }
```
![](https://hackmd.io/_uploads/rkIwZI1In.gif)

---
跟滑鼠移動，及物件移動速度
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

// class:類別
class Obj {  //宣告一個類別，針對一個畫的圖案
   constructor(args){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
      // this.p = args.p || {x:random(width),y:random(height)} // 描述為該物件的初始位置
      this.p = args.p || createVector(random(width),random(height)) //用"向量"方式呈現
      // this.v = {x:random(-1,1),y:random(-1,1)} //物件的移動速度
      this.v = createVector(random(-1,1),random(-1,1)) 
      this.size = random(8,12) //物件的放大倍率
      this.color = random(fill_colors) //充滿顏色
      this.stroke = random(line_colors) //外框線條顏色
   }
   draw(){ 
    push() //執行push()後，依照設定，設定原點(0,0)的位置
      translate(this.p.x,this.p.y) //以該物件位置為原點
      scale(this.v.x<0?1:-1,-1)    //X軸的放大倍率，如果this.v.x<0條件成立，值為1，否則為-1；Y軸的-1，為上下翻轉
      fill(this.color) 
      stroke(this.stroke)
      strokeWeight(4)//線條粗細
      beginShape()
      for(var k=0; k <points.length; k=k+1){
        // line(points[k][0]*this.size,points[k][1]*this.size,points[k+1][0]*this.size,points[k+1][1]*this.size) //需要提供2個點的座標
        // vertex(points[k][0]*this.size,points[k][1]*this.size) //只要設定一個點，當指令到endshape()，會把所有的點串接再一起
        curveVertex(points[k][0]*this.size,points[k][1]*this.size) //畫線為圓弧方式畫圖
      }
      endShape()
    pop() //執行pop()，原點(0,0)設定回到整個視窗的左上方
   }
   update(){ //移動的程式內容
    // this.p.x = this.p.x +this.v.x //x軸目前的位置(this.p.x)加上X軸移動速度(this.v.x)
    // this.p.y = this.p.y +this.v.y //y軸目前的位置(this.p.y)加上y軸移動速度(this.v.y)
    this.p.add(this.v) //設定好向量後，使用add，就可以與上面2行指令相同
    //向量sub==>減號

    //--------------------知道滑鼠的位置，並建立一個滑鼠的向量-------------------------------
    let mouseV = createVector(mouseX,mouseY) //把滑鼠位置轉換為一個向量值
    let delta = mouseV.sub(this.p).limit(this.v.mag()*2)//sub計算出滑鼠所在位置向量(mouseV)到物件向量(this.p)
    //this.v.mag()代表該物見的速度大小(一個向量值有大小及方向)
    this.p.add(delta)
    //-----------------------------------------------------------------------------------------

    if(this.p.x<=0 || this.p.x>=width){ //碰到X軸左邊(<=0)，或是碰到右邊(>=width)
      this.v.x = -this.v.x        //把速度方向改變
    }
    if(this.p.y<=0 || this.p.y>=height){ //碰到y軸上邊(<=0)，或是碰到下邊(>=height)
      this.v.y = -this.v.y        //把速度方向改變
    }
   }
   isBallInRanger(){ //判斷滑鼠按下的位置，是否在物件範圍內
    let d = dist(mouseX,mouseY,this.p.x,this.p.y) //計算(mouseX,mouseY)和(this.p.x,this.p.y)兩點的距離
    if(d<4*this.size){
      return true   //滑鼠與物件的距離<物件寬度，代表碰觸了，傳回true值
    }else{
      return false  //滑鼠與物件的距離>物件寬度，代表沒有碰觸，傳回false值
    }
   }
}

var ball  //"目前要處理"的物件，暫時放在ball變數內
var balls =[] //產生更多物件
var score = 0

function setup() {
  createCanvas(windowWidth, windowHeight);
  for(var i=0;i<60;i=i+1){ // i=0,1,2,3,4,...59，i的數課可以任調
    ball = new Obj({}) //產生一個Obj class元件
    balls.push(ball) //把ball的物件放入到balls陣列內
  }
}


function draw() {
  background(220);
//  for(var j=0;j<balls.length;j=j+1){
//   ball =balls[j]
//   ball.draw()
//   ball.update()
//  }

 for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
 {
   ball.draw()
   ball.update()
 }
 textSize(50)
 text(score,50,50)//在座標(50,50)上，顯示score分數內容

}


function mousePressed(){

  //++++++++++產生一個物件+++++++++++++++++++++++++++++++++++
  // ball = new Obj({
  //   p:{x:mouseX, y:mouseY}
  // }) //在滑鼠按下的地方，產生一個新的Obj class元件
  // balls.push(ball) //把ball的物件放入到balls陣列內
  //+++++++++++++++++++++++++++++++++++++++++++++++++++++++++


  //----------在物件上按下滑鼠，物件消失，分數+1---------------------------
  for(let ball of balls){ //檢查每一個物件
    if(ball.isBallInRanger()){ 
      balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
      score = score + 1
    }
  }
}
```
![](https://hackmd.io/_uploads/rk3EMLkU3.gif)

---
在中間畫一個砲台跟著滑鼠移動
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

  // class:類別
  class Obj {  //宣告一個類別，針對一個畫的圖案
     constructor(args){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
        // this.p = args.p || {x:random(width),y:random(height)} // 物件的初始位置
        this.p = args.p || createVector(random(width),random(height)) //用"向量"方式呈現
        // this.v = {x:random(-1,1),y:random(-1,1)} //物件的移動速度
        this.v = createVector(random(-1,1),random(-1,1)) 
        this.size = random(8,12) //物件的放大倍率
        this.color = random(fill_colors) //充滿顏色
        this.stroke = random(line_colors) //外框線條顏色
     }
     draw(){ 
      push() //執行push()後，依照設定，設定原點(0,0)的位置
        translate(this.p.x,this.p.y) //以該物件位置為原點
        scale(this.v.x<0?1:-1,-1)    //X軸的放大倍率，如果this.v.x<0條件成立，值為1，否則為-1；Y軸的-1，為上下翻轉
        fill(this.color) 
        stroke(this.stroke)
        strokeWeight(4)//線條粗細
        beginShape()
        for(var k=0; k <points.length; k=k+1){
          // line(points[k][0]*this.size,points[k][1]*this.size,points[k+1][0]*this.size,points[k+1][1]*this.size) //需要提供2個點的座標
          // vertex(points[k][0]*this.size,points[k][1]*this.size) //只要設定一個點，當指令到endshape()，會把所有的點串接再一起
          curveVertex(points[k][0]*this.size,points[k][1]*this.size) //畫線為圓弧方式畫圖
        }
        endShape()
      pop() //執行pop()，原點(0,0)設定回到整個視窗的左上方
     }
     update(){ //移動的程式內容
      // this.p.x = this.p.x +this.v.x //x軸目前的位置(this.p.x)加上X軸移動速度(this.v.x)
      // this.p.y = this.p.y +this.v.y //y軸目前的位置(this.p.y)加上y軸移動速度(this.v.y)
      this.p.add(this.v) //設定好向量後，使用add，就可以與上面2行指令相同
      //向量sub==>減號
  
      //--------------------知道滑鼠的位置，並建立一個滑鼠的向量-------------------------------
      let mouseV = createVector(mouseX,mouseY) //把滑鼠位置轉換為一個向量值
      let delta = mouseV.sub(this.p).limit(this.v.mag()*2)//sub計算出滑鼠所在位置向量(mouseV)到物件向量(this.p)
      //this.v.mag()代表該物見的速度大小(一個向量值有大小及方向)
      this.p.add(delta)
      //-----------------------------------------------------------------------------------------
  
      if(this.p.x<=0 || this.p.x>=width){ //碰到X軸左邊(<=0)，或是碰到右邊(>=width)
        this.v.x = -this.v.x        //把速度方向改變
      }
      if(this.p.y<=0 || this.p.y>=height){ //碰到y軸上邊(<=0)，或是碰到下邊(>=height)
        this.v.y = -this.v.y        //把速度方向改變
      }
     }
     isBallInRanger(){ //判斷滑鼠按下的位置，是否在物件範圍內
      let d = dist(mouseX,mouseY,this.p.x,this.p.y) //計算(mouseX,mouseY)和(this.p.x,this.p.y)兩點的距離
      if(d<4*this.size){
        return true   //滑鼠與物件的距離<物件寬度，代表碰觸了，傳回true值
      }else{
        return false  //滑鼠與物件的距離>物件寬度，代表沒有碰觸，傳回false值
      }
     }
  }
  
 

  var ball  //"目前要處理"的物件，暫時放在ball變數內
  var balls =[] //產生更多物件
  var score = 0
  
  function setup() {
    createCanvas(windowWidth, windowHeight);
    for(var i=0;i<30;i=i+1){ 
      ball = new Obj({}) //產生一個Obj class元件
      balls.push(ball) //把ball的物件放入到balls陣列內
    }
  }
  
  
  function draw() {
    background(220);
  //  for(var j=0;j<balls.length;j=j+1){
  //   ball =balls[j]
  //   ball.draw()
  //   ball.update()
  //  }
  
   for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
   {
     ball.draw()
     ball.update()
   }
   textSize(50)
   text(score,50,50)//在座標(50,50)上，顯示score分數內容
   push()  //重新規劃原點(0,0)，在視窗的中間
     let dx = mouseX - width/2 //滑鼠
     let dy = mouseY - height/2 //滑鼠
     let angle = atan2(dy,dx) //跟著滑鼠移動
     translate(width/2,height/2)
     fill("#aec5eb")
     noStroke()
     rotate(angle)
     triangle(-25,25,-25,-25,50,0) //設定三個點，畫成一個三角形
     ellipse(0,0,50)
   pop()  //恢復原本設定，原點在(0,0)在視窗的左上角
  }
  
  
  function mousePressed(){
  
    //++++++++++產生一個物件+++++++++++++++++++++++++++++++++++
    // ball = new Obj({
    //   p:{x:mouseX, y:mouseY}
    // }) //在滑鼠按下的地方，產生一個新的Obj class元件
    // balls.push(ball) //把ball的物件放入到balls陣列內
    //+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
  
  
    //----------在物件上按下滑鼠，物件消失，分數+1---------------------------
    for(let ball of balls){ //檢查每一個物件
      if(ball.isBallInRanger()){ 
        balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
        score = score + 1
      }
    }
    //-----------------------------------------------------------------------
  
  }

```
---
創設資料夾
---
![](https://hackmd.io/_uploads/S1iGwG5N3.png)

### 記得這裡要加(紅圈)的東西
![](https://hackmd.io/_uploads/rychLIkL2.png)

---
# 發射子彈
---


![](https://hackmd.io/_uploads/SJ9ESwJLn.gif)
---
發射子彈(sketch.js的檔)
---

```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

 //++++++++++設定畫points所有"點"的物件變數
  var ball 
  var balls=[]
  //+++++++++++++++++++++++++++++++++

  //++++++++++++++++設定飛彈物件變數
  var bullet
  var bullets =[]
  //+++++++++++++++++++++++++

  var score =0
  
  function setup() {
    createCanvas(windowWidth, windowHeight);
    for(var i=0;i<30;i=i+1){ // i的數課可以任調
      ball = new Obj({}) //產生一個Obj class元件
      balls.push(ball) //把ball的物件放入到balls陣列內
    }
  }
  
  
  function draw() {
    background(220);
  //  for(var j=0;j<balls.length;j=j+1){
  //   ball =balls[j]
  //   ball.draw()
  //   ball.update()
  //  }

  //++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
  //貓咪顯示
   for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
   {
     ball.draw()
     ball.update()
     for(let bullet of bullets){ 
        if(ball.isBallInRanger(bullet.p.x,bullet.p.y)){   //物件有無接觸現在的ball 
          balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
          bullets.splice(bullets.indexOf(bullet),1) 
          score = score + 1
        }
      }
   }
 
  //飛彈顯示
   for(let bullet of bullets) //只要是陣列方式，都可以利用此方式處理
   {
     bullet.draw()
     bullet.update()
   }
  //++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
   textSize(50)
   text(score,50,50)//在座標(50,50)上，顯示score分數內容
   push()  //重新規劃原點(0,0)，在視窗的中間
     let dx = mouseX - width/2 //滑鼠
     let dy = mouseY - height/2 //滑鼠
     let angle = atan2(dy,dx) //跟著滑鼠移動
     translate(width/2,height/2)
     fill("#aec5eb")
     noStroke()
     rotate(angle)
     triangle(-25,25,-25,-25,50,0) //設定三個點，畫成一個三角形
     ellipse(0,0,50)
   pop()  //恢復原本設定，原點在(0,0)在視窗的左上角
  }
  
  
  function mousePressed(){
  
    //++++++++++產生一個物件+++++++++++++++++++++++++++++++++++
    // ball = new Obj({
    //   p:{x:mouseX, y:mouseY}
    // }) //在滑鼠按下的地方，產生一個新的Obj class元件
    // balls.push(ball) //把ball的物件放入到balls陣列內
    //+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
  
  
    //----------在物件上按下滑鼠，物件消失，分數+1---------------------------
    // for(let ball of balls){ //檢查每一個物件
    //   if(ball.isBallInRanger()){ 
    //     balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
    //     score = score + 1
    //   }
    // }
    //-----------------------------------------------------------------------
   
    //++++++++++++++按一下產生一個飛彈++++++++++++++++++++++++++++++++++++++
    bullet = new Bullet({
      r:20
    }) //在滑鼠按下的地方，產生一個bullet class 元件(產生一個飛彈)
    bullets.push(bullet)    //把bullet的物件放到bullets陣列內
  }
  

 ```
 
 ---
發射子彈(bullet.js的檔)
---
```javascript=
class Bullet{
    constructor(args){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
        this.r = args.r || 10  //設計飛彈有大有小時，就傳參數，args.r來設定飛彈大小，沒有參數就以10為主
        this.p = args.p ||createVector(width/2,height/2)    //建立一個向量{x:width/2, y:height/2}
        this.v = args.v ||createVector(mouseX-width/2,mouseY-height/2).limit(10)
        this.color = args.color || "#e4c1f9"

    }
    draw(){ //繪出物件
        push()
             translate(this.p.x,this.p.y)
             fill(this.color)
             noStroke()
            ellipse(0,0,this.r)
        pop()
    }
    update(){ //計算出移動後的位置
        this.p.add(this.v)
    }

}

```
 
 ---
發射子彈(obj.js檔)
---
```javascript=
class Obj {  //宣告一個類別，針對一個畫的圖案
    constructor(args){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
       // this.p = args.p || {x:random(width),y:random(height)} // 描述為該物件的初始位置
       this.p = args.p || createVector(random(width),random(height)) //用"向量"方式呈現
       // this.v = {x:random(-1,1),y:random(-1,1)} //物件的移動速度
       this.v = createVector(random(-1,1),random(-1,1)) 
       this.size = random(15,20) //物件的放大倍率
       this.color = random(fill_colors) //充滿顏色
       this.stroke = random(line_colors) //外框線條顏色
    }
    draw(){ 
     push() //執行push()後，依照設定，設定原點(0,0)的位置
       translate(this.p.x,this.p.y) //以該物件位置為原點
       scale(this.v.x<0?1:-1,-1)    //X軸的放大倍率，如果this.v.x<0條件成立，值為1，否則為-1；Y軸的-1，為上下翻轉
       fill(this.color) 
       stroke(this.stroke)
       strokeWeight(4)//線條粗細
       beginShape()
       for(var k=0; k <points.length; k=k+1){
         // line(points[k][0]*this.size,points[k][1]*this.size,points[k+1][0]*this.size,points[k+1][1]*this.size) //需要提供2個點的座標
         // vertex(points[k][0]*this.size,points[k][1]*this.size) //只要設定一個點，當指令到endshape()，會把所有的點串接再一起
         curveVertex(points[k][0]*this.size,points[k][1]*this.size) //畫線為圓弧方式畫圖
       }
       endShape()
     pop() //執行pop()，原點(0,0)設定回到整個視窗的左上方
    }
    update(){ //移動的程式內容
     // this.p.x = this.p.x +this.v.x //x軸目前的位置(this.p.x)加上X軸移動速度(this.v.x)
     // this.p.y = this.p.y +this.v.y //y軸目前的位置(this.p.y)加上y軸移動速度(this.v.y)
     this.p.add(this.v) //設定好向量後，使用add，就可以與上面2行指令相同
     //向量sub==>減號
 
     //--------------------知道滑鼠的位置，並建立一個滑鼠的向量-------------------------------
     let mouseV = createVector(mouseX,mouseY) //把滑鼠位置轉換為一個向量值
     let delta = mouseV.sub(this.p).limit(this.v.mag()*2)//sub計算出滑鼠所在位置向量(mouseV)到物件向量(this.p)
     //this.v.mag()代表該物見的速度大小(一個向量值有大小及方向)
     this.p.add(delta)
     //-----------------------------------------------------------------------------------------
 
     if(this.p.x<=0 || this.p.x>=width){ //碰到X軸左邊(<=0)，或是碰到右邊(>=width)
       this.v.x = -this.v.x        //把速度方向改變
     }
     if(this.p.y<=0 || this.p.y>=height){ //碰到y軸上邊(<=0)，或是碰到下邊(>=height)
       this.v.y = -this.v.y        //把速度方向改變
     }
    }
    isBallInRanger(x,y){ //判斷滑鼠按下的位置，是否在物件範圍內
     let d = dist(x,y,this.p.x,this.p.y) //計算(mouseX,mouseY)和(this.p.x,this.p.y)兩點的距離
     if(d<4*this.size){
       return true   //滑鼠與物件的距離<物件寬度，代表碰觸了，傳回true值
     }else{
       return false  //滑鼠與物件的距離>物件寬度，代表沒有碰觸，傳回false值
     }
    }
 }

```
![](https://hackmd.io/_uploads/SJ9ESwJLn.gif)
---
## 加入音樂(sketch.js檔的程式碼)
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

 //++++++++++設定畫points所有"點"的物件變數
  var ball 
  var balls=[]
  //+++++++++++++++++++++++++++++++++S

  //++++++++++++++++設定飛彈物件變數
  var bullet
  var bullets =[]
  //+++++++++++++++++++++++++

  var score =0


  function preload(){ //加入音樂
    cat_sound = loadSound("音樂/cat3b.mp3")
    bullet_sound = loadSound("音樂/jump13.mp3")
  }


  function setup() {
    createCanvas(windowWidth, windowHeight);
    for(var i=0;i<30;i=i+1){ // i的數課可以任調
      ball = new Obj({}) //產生一個Obj class元件
      balls.push(ball) //把ball的物件放入到balls陣列內
    }
  }
  
  
  function draw() {
    background(220);
  //  for(var j=0;j<balls.length;j=j+1){
  //   ball =balls[j]
  //   ball.draw()
  //   ball.update()
  //  }

  //++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
  //貓咪顯示
   for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
   {
     ball.draw()
     ball.update()
     for(let bullet of bullets){ 
        if(ball.isBallInRanger(bullet.p.x,bullet.p.y)){   //物件有無接觸現在的ball 
          balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
          bullets.splice(bullets.indexOf(bullet),1) 
          score = score + 1
          cat_sound.play()

        }
      }
   }
 
  //飛彈顯示
   for(let bullet of bullets) //只要是陣列方式，都可以利用此方式處理
   {
     bullet.draw()
     bullet.update()
   }
  //++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
   textSize(50)
   text(score,50,50)//在座標(50,50)上，顯示score分數內容
   push()  //重新規劃原點(0,0)，在視窗的中間
     let dx = mouseX - width/2 //滑鼠
     let dy = mouseY - height/2 //滑鼠
     let angle = atan2(dy,dx) //跟著滑鼠移動
     translate(width/2,height/2)
     fill("#aec5eb")
     noStroke()
     rotate(angle)
     triangle(-25,25,-25,-25,50,0) //設定三個點，畫成一個三角形
     ellipse(0,0,50)
   pop()  //恢復原本設定，原點在(0,0)在視窗的左上角
  }
  
  
  function mousePressed(){
  
    //++++++++++產生一個物件+++++++++++++++++++++++++++++++++++
    // ball = new Obj({
    //   p:{x:mouseX, y:mouseY}
    // }) //在滑鼠按下的地方，產生一個新的Obj class元件
    // balls.push(ball) //把ball的物件放入到balls陣列內
    //+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
  
  
    //----------在物件上按下滑鼠，物件消失，分數+1---------------------------
    // for(let ball of balls){ //檢查每一個物件
    //   if(ball.isBallInRanger()){ 
    //     balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
    //     score = score + 1
    //   }
    // }
    //-----------------------------------------------------------------------
   
    //++++++++++++++按一下產生一個飛彈++++++++++++++++++++++++++++++++++++++
    bullet = new Bullet({}) //在滑鼠按下的地方，產生一個bullet class 元件(產生一個飛彈)
    bullets.push(bullet)    //把bullet的物件放到bullets陣列內
    bullet_sound.play()
  }
  
```
![](https://hackmd.io/_uploads/rJQh57V82.gif)
---
## 設定怪物(sketch.js檔)
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

 //++++++++++設定畫points所有"點"的物件變數
  var ball 
  var balls=[]
  //++++++++++++++++設定飛彈物件變數
  var bullet
  var bullets =[]
  //++++++++++++++++設定怪物的物件變數
  //設定怪物的物件變數
  var monster //把目前要處理的物件，暫存到bullet變數內
  var monsters = [] //把產生的"所有"物件，為物件的倉庫，所有的物件資料都在此

  var score =0


  function preload(){ //加入音樂
    cat_sound = loadSound("音樂/cat3b.mp3")
    bullet_sound = loadSound("音樂/jump13.mp3")
  }


  function setup() {
    createCanvas(windowWidth, windowHeight);
    for(var i=0;i<30;i=i+1){ // i的數課可以任調
      ball = new Obj({}) //產生一個Obj class元件
      balls.push(ball) //把ball的物件放入到balls陣列內
    }
    for(var i=0;i<10;i=i+1){
      monster = new Monster({}) //產生一個Obj class元件
      monsters.push(monster) //把ball的物件放入到balls陣列內
    }
  }
  
  
  function draw() {
    background(220);
  //  for(var j=0;j<balls.length;j=j+1){
  //   ball =balls[j]
  //   ball.draw()
  //   ball.update()
  //  }

  //貓咪顯示
   for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
   {
     ball.draw()
     ball.update()
     for(let bullet of bullets){ 
        if(ball.isBallInRanger(bullet.p.x,bullet.p.y)){   //物件有無接觸現在的ball 
          balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
          bullets.splice(bullets.indexOf(bullet),1) 
          score = score + 1
          cat_sound.play()
        }
      }
   }
 
  //飛彈顯示
   for(let bullet of bullets) //只要是陣列方式，都可以利用此方式處理
   {
     bullet.draw()
     bullet.update()
   }
   //怪物的顯示(monster)
   for(let monster of monsters){ //只要是陣列的方式，都可以利用此方式處理
     monster.draw()
     monster.update()
   }
 
  push()
    fill(255)
    textSize(50)
    text(score,50,50)//在座標(50,50)上，顯示score分數內容
  pop()

  push()  //開始設定
     let dx = mouseX - width/2 //滑鼠
     let dy = mouseY - height/2 //滑鼠
     let angle = atan2(dy,dx) //跟著滑鼠移動
       translate(width/2,height/2)
       fill("#aec5eb")
       noStroke()
       rotate(angle)
       triangle(-25,25,-25,-25,50,0) //設定三個點，畫成一個三角形
       ellipse(0,0,50)
  pop()  //設定恢復原樣
  }
  
  
    // function mousePressed(){
    // for(let ball of balls){ //檢查每一個物件
    //   if(ball.isBallInRanger()){ 
    //     balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
    //     score = score + 1
    //   }
    // }
    
    //++++++++++++++按一下產生一個飛彈++++++++++++++++++++++++++++++++++++++
    function mousePressed(){ 
    bullet = new Bullet({}) //在滑鼠按下的地方，產生一個bullet class 元件(產生一個飛彈)
    bullets.push(bullet)    //把bullet的物件放到bullets陣列內
    bullet_sound.play()
  }
  

```

---
## 設定怪物(monster.js檔的程式碼)
---
```javascript=
var monster_colors = "e6ccb2-ddb892-b08968-7f5539-9c6644".split("-").map(a=>"#"+a)

class Monster {
  constructor(args) {
    this.r = args.r || random(50,100)
    this.p = args.p || createVector(random(0+this.r,width-this.r), random(0+this.r,height-this.r))
    this.v = args.v || createVector(random(-1,1), random(-1,1))
    this.color = args.color || random(monster_colors)
    this.mode = random(["happy","bad"])
  }
  
  draw() {
    push();
    translate(this.p.x, this.p.y);
    fill(this.color);
    noStroke();
    
    // 绘制星星形状
    beginShape();
    for (var i = 0; i < 10; i++) {
      var angle = map(i, 0, 10, 0, TWO_PI);
      var x = cos(angle) * this.r;
      var y = sin(angle) * this.r;
      vertex(x, y);
      var angle2 = map(i + 0.5, 0, 10, 0, TWO_PI);
      var x2 = cos(angle2) * (this.r / 2);
      var y2 = sin(angle2) * (this.r / 2);
      vertex(x2, y2);
    }
    endShape(CLOSE);
    
    if (this.mode == "happy") {
      fill(255);
      ellipse(0, 0, this.r/2);
      fill(0);
      ellipse(0, 0, this.r/3);
    } else {
      fill(255);
      arc(0, 0, this.r/2, this.r/2, 0, PI);
      fill(0);
      arc(0, 0, this.r/3, this.r/3, 0, PI);
    }
    
    pop();
  }

  update() {
    this.p.add(this.v);

    if (this.p.x <= 0 + this.r || this.p.x >= width - this.r) {
      this.v.x = -this.v.x;
    }
    if (this.p.y <= 0 + this.r || this.p.y >= height - this.r) {
      this.v.y = -this.v.y;
    }
  }
}

```
![](https://hackmd.io/_uploads/HyIiI4E82.gif)


---
# 砲台上下左右移動

#### sketch.js
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

 //++++++++++設定畫points所有"點"的物件變數
  var ball 
  var balls=[]
  //++++++++++++++++設定飛彈物件變數
  var bullet
  var bullets =[]
  //++++++++++++++++設定怪物的物件變數
  //設定怪物的物件變數
  var monster //把目前要處理的物件，暫存到bullet變數內
  var monsters = [] //把產生的"所有"物件，為物件的倉庫，所有的物件資料都在此
  var score =0 //分數
  var shipP//設定砲台位移

  function preload(){ //加入音樂
    cat_sound = loadSound("音樂/cat3b.mp3")
    bullet_sound = loadSound("音樂/jump13.mp3")
    monster_sound = loadSound("音樂/devil_groaning2.mp3")
  }


  function setup() {
    createCanvas(windowWidth, windowHeight);
    shipP = createVector(width/2,height/2)
    for(var i=0;i<20;i=i+1){ 
      ball = new Obj({}) //產生一個Obj class元件
      balls.push(ball) //把ball的物件放入到balls陣列內
    }
    for(var i=0;i<10;i=i+1){
      monster = new Monster({}) //產生一個Obj class元件
      monsters.push(monster) //把ball的物件放入到balls陣列內
    }
  }
  
  
  function draw() {
    background(220);
  //  for(var j=0;j<balls.length;j=j+1){
  //   ball =balls[j]
  //   ball.draw()
  //   ball.update()
  //  }

  if(keyIsPressed){
    if(key=="ArrowRight" || key=="d"){ //下往右鍵或d往右移動
      shipP.x = shipP.x+5
    }
  
    if(key=="ArrowLeft" || key=="a"){ //按往左鍵或a往左移動0
      shipP.x = shipP.x-5
    }
  
    if(key=="ArrowUp" || key=="w"){ //按往上鍵或w往上移動
      shipP.y = shipP.y-5
    }
  
    if(key=="ArrowDown" || key=="s"){ //按往下鍵或s往下移動
      shipP.y = shipP.y+5
    }

  }


  //貓咪顯示
   for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
   {
     ball.draw()
     ball.update()
     for(let bullet of bullets){ 
        if(ball.isBallInRanger(bullet.p.x,bullet.p.y)){   //物件有無接觸現在的ball 
          balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
          bullets.splice(bullets.indexOf(bullet),1) 
          score = score - 1
          cat_sound.play()
        }
      }
   }
 
  //飛彈顯示
   for(let bullet of bullets) //只要是陣列方式，都可以利用此方式處理
   {
     bullet.draw()
     bullet.update()
   }
   //怪物的顯示(monster)
   for(let monster of monsters){ //只要是陣列的方式，都可以利用此方式處理
     monster.draw()
     monster.update()
     for(let bullet of bullets){ //檢查每一個物件
      if(monster.isMonsterInRanger(bullet.p.x,bullet.p.y)){ //飛彈物件有沒有接觸現在的ball
        monsters.splice(monsters.indexOf(monster),1) //從倉庫balls裡取出被滑鼠按到的物件編號(balls.indexOf(ball),1)，只取一個
        bullets.splice(bullets.indexOf(bullet),1)         
        score = score + 2 
        monster_sound.play()
      }
    }
   }
 
  push()
    fill(255)
    textSize(50)
    text(score,50,50)//在座標(50,50)上，顯示score分數內容
  pop()

  push()  //開始設定
     let dx = mouseX - width/2 //滑鼠
     let dy = mouseY - height/2 //滑鼠
     let angle = atan2(dy,dx) //跟著滑鼠移動
        translate(shipP.x,shipP.y)
        noStroke()
        rotate(angle)
        fill("#cdb4db")
        ellipse(0,0,50)
        fill("#ffafcc")
        triangle(-25,25,-25,-25,50,0) //設定三個點，畫成三角形
  pop()  //設定恢復原樣
  }
  
  
    // function mousePressed(){
    // for(let ball of balls){ //檢查每一個物件
    //   if(ball.isBallInRanger()){ 
    //     balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
    //     score = score + 1
    //   }
    // }
    
    //++++++++++++++按一下產生一個飛彈++++++++++++++++++++++++++++++++++++++
    function mousePressed(){ 
    bullet = new Bullet({}) //在滑鼠按下的地方，產生一個bullet class 元件(產生一個飛彈)
    bullets.push(bullet)    //把bullet的物件放到bullets陣列內
    bullet_sound.play()
  }
    function keyPressed(){
      if(key==" "){ //按下空白鍵
        bullet = new Bullet({}) //在滑鼠按下的地方產生一個新的飛彈(Bullet class)
        bullets.push(bullet)
        bullet_sound.play()
    }
  }



```
#### monster.js
---
```javascript=
var monster_colors = "ede0d4-e6ccb2-ddb892-b08968-7f5539-9c6644".split("-").map(a=>"#"+a)

class Monster {
  constructor(args) {
    this.r = args.r || random(50,100)
    this.p = args.p || createVector(random(0+this.r,width-this.r), random(0+this.r,height-this.r))
    this.v = args.v || createVector(random(-1,1), random(-1,1))
    this.color = args.color || random(monster_colors)
    this.mode = random(["happy","bad"])
  }
  
  draw() {
    push();
    translate(this.p.x, this.p.y);
    fill(this.color);
    noStroke();
    
    // 绘制星星形状
    beginShape();
    for (var i = 0; i < 25; i++) {
      var angle = map(i, 0, 10, 0, TWO_PI);
      var x = cos(angle) * this.r;
      var y = sin(angle) * this.r;
      vertex(x, y);
      var angle2 = map(i + 0.5, 0, 10, 0, TWO_PI);
      var x2 = cos(angle2) * (this.r / 2);
      var y2 = sin(angle2) * (this.r / 2);
      vertex(x2, y2);
    }
    endShape(CLOSE);
    
    if (this.mode == "happy") {
      fill(255);
      ellipse(0, 0, this.r/2);
      fill(0);
      ellipse(0, 0, this.r/3);
    } else {
      fill(255);
      arc(0, 0, this.r/2, this.r/2, 0, PI);
      fill(0);
      arc(0, 0, this.r/3, this.r/3, 0, PI);
    }
    
    pop();
  }

  update() {
    this.p.add(this.v);

    if (this.p.x <= 0 + this.r || this.p.x >= width - this.r) {
      this.v.x = -this.v.x;
    }
    if (this.p.y <= 0 + this.r || this.p.y >= height - this.r) {
      this.v.y = -this.v.y;
    }
  }



isMonsterInRanger(x,y){ //功能:判斷飛彈位置是否移動到此物件的範圍內
  let d = dist(x,y,this.p.x,this.p.y) //計算兩點(滑鼠按下與物件中心點)之間的距離，放到d變數內
  if(d<this.r/2){ //滑鼠與物件的距離小於物件的寬度，代表碰到了
    return true //傳回true的值
  }else{ //滑鼠與物件的距離大於物件的寬度，代表沒有碰到
    return false //傳回false值
  }
}
}

```
#### bullet.js
---
```javascript=
class Bullet{
    constructor(args){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
        this.r = args.r || 10  //設計飛彈有大有小時，就傳參數，args.r來設定飛彈大小，沒有參數就以10為主
        this.p = args.p ||createVector(width/2,height/2)    //建立一個向量{x:width/2, y:height/2}
        this.v = args.v ||createVector(mouseX-width/2,mouseY-height/2).limit(10)
        this.color = args.color || "#e4c1f9"

    }
    draw(){ //繪出物件
        push()
             translate(this.p.x,this.p.y)
             fill(this.color)
             noStroke()
            ellipse(0,0,this.r)
        pop()
    }
    update(){ //計算出移動後的位置
        this.p.add(this.v)
    }

}
```
#### obj.js
---
```javascript=
class Obj{ //宣告一個類別，針對一個畫的圖案
  constructor(args){ //預設值，基本資料(物件的顏色，移動速度，大小，初始位置......)
    // this.p = args.p || { x:random(0,width), y:random(0,height) } //描述為該物件的初始位置，||(or)，當產生一個物件時，有傳位置參數的話使用該參數，若沒有傳參數就以||後面的設定產出
    this.p = args.p || createVector(random(0,width),random(0,height)) //效果等同上面那行，把原本的{x:..., y:...}改成"向量"方式呈現

    // this.v = { x:random(-1,1), y:random(-1,1) } //描述為該物件的移速
    this.v = createVector(random(-1,1),random(-1,1)) //效果等同上面那行，把原本的{x:..., y:...}改成"向量"方式呈現

    this.size = random(5,10) //描述為該物件的放大倍率
    this.color = random(fill_colors) //充滿顏色
    this.stroke = random(line_colors) //外框線條顏色
  }

  draw(){ //畫出單一個物件形狀
    push() //執行後，依照以下設定
      translate(this.p.x,this.p.y) //以讓物件位置為原點
      scale(this.v.x<0?-1:1,-1) //如果this.v.x<0條件成立，則為1，若不成立，則為-1；代表往右走的圖形象鼻向右，向左的則象鼻向左
      fill(this.color)
      stroke(this.stroke)
      strokeWeight(4)
      beginShape()
        for(var k=0;k<points.length;k=k+1){
          // line(points[k][0]*this.size,points[k][1]*this.size,points[k+1][0]*this.size,points[k+1][1]*this.size)
          // vertex(points[k][0]*this.size,points[k][1]*this.size) //只要設定一個點，當指令到endShape()，會把所有點連在一起，要把上面迴圈points.length-1的-1留著
          curveVertex(points[k][0]*this.size,points[k][1]*this.size) //畫圖為圓弧方式畫，要把上面迴圈points.length-1的-1刪除
        }
      endShape()
    pop() //執行後，回到原始的設定
  }

  update(){ //圖形的移動
    // this.p.x = this.p.x + this.v.x //現在的位置(x)加上現在的速度(x)
    // this.p.y = this.p.y + this.v.y //現在的位置(y)加上現在的速度(y)
    this.p.add(this.v) //設定好向量後才能使用(CreateVector)，可以取代上面兩行指令，效果不變
    //向量sub==>減號

    //知道滑鼠的位置，並建立一個滑鼠的向量
    // let mouseV = createVector(mouseX,mouseY) //把滑鼠的位置轉換成一個向量值
    // let delta = mouseV.sub(this.p).limit(this.v.mag()*1.5) //sub計算滑鼠所在位置向量(mouseV)到物件向量(this.p)的距離，limit(this.v.mag())意思為每次距離縮短(慢慢移動)，mag意思為取得大小，*1.5為速度加快幾倍
    // this.p.add(delta)

    if(this.p.x<=0 || this.p.x>=width){ //x軸碰到左邊(<=0)或者碰到右邊(x>=width)
      this.v.x = -this.v.x //把x軸的速度方向改變
    }
    if(this.p.y<=0 || this.p.y>=height){ //y軸碰到左邊(<=0)或者碰到右邊(x>=width)
      this.v.y = -this.v.y //把y軸的速度方向改變
    }
  }

  isBallInRanger(x,y){ //功能:判斷滑鼠按下的位置是否在此物件的範圍內
    let d = dist(x,y,this.p.x,this.p.y) //計算兩點(滑鼠按下與物件中心點)之間的距離，放到d變數內
    if(d<13*this.size){ //滑鼠與物件的距離小於物件的寬度，代表碰到了
      return true //傳回true的值
    }else{ //滑鼠與物件的距離大於物件的寬度，代表沒有碰到
      return false //傳回false值
    }
  }
}

```
![](https://hackmd.io/_uploads/S1aZIqEU3.gif)
---
# 打中後變形消失

#### sketch.js
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

 //++++++++++設定畫points所有"點"的物件變數
  var ball 
  var balls=[]
  //++++++++++++++++設定飛彈物件變數
  var bullet
  var bullets =[]
  //++++++++++++++++設定怪物的物件變數
  //設定怪物的物件變數
  var monster //把目前要處理的物件，暫存到bullet變數內
  var monsters = [] //把產生的"所有"物件，為物件的倉庫，所有的物件資料都在此
  var score =0 //分數
  var shipP//設定砲台位移

  function preload(){ //加入音樂
    cat_sound = loadSound("mousic/cat3b.mp3")
    bullet_sound = loadSound("mousic/jump13.mp3")
    monster_sound = loadSound("mousic/destruction1.mp3")
  }


  function setup() {
    createCanvas(windowWidth, windowHeight);
    shipP = createVector(width/2,height/2)
    for(var i=0;i<20;i=i+1){ 
      ball = new Obj({}) //產生一個Obj class元件
      balls.push(ball) //把ball的物件放入到balls陣列內
    }
    for(var i=0;i<10;i=i+1){
      monster = new Monster({}) //產生一個Obj class元件
      monsters.push(monster) //把ball的物件放入到balls陣列內
    }
  }
  
  
  function draw() {
    background(220);
  //  for(var j=0;j<balls.length;j=j+1){
  //   ball =balls[j]
  //   ball.draw()
  //   ball.update()
  //  }

  if(keyIsPressed){
    if(key=="ArrowRight" || key=="d"){ //下往右鍵或d往右移動
      shipP.x = shipP.x+5
    }
  
    if(key=="ArrowLeft" || key=="a"){ //按往左鍵或a往左移動0
      shipP.x = shipP.x-5
    }
  
    if(key=="ArrowUp" || key=="w"){ //按往上鍵或w往上移動
      shipP.y = shipP.y-5
    }
  
    if(key=="ArrowDown" || key=="s"){ //按往下鍵或s往下移動
      shipP.y = shipP.y+5
    }

  }


  //貓咪顯示
   for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
   {
     ball.draw()
     ball.update()
     for(let bullet of bullets){ 
        if(ball.isBallInRanger(bullet.p.x,bullet.p.y)){   //物件有無接觸現在的ball 
          balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
          bullets.splice(bullets.indexOf(bullet),1) 
          score = score - 1
          cat_sound.play()
        }
      }
   }
 
  //飛彈顯示
   for(let bullet of bullets) //只要是陣列方式，都可以利用此方式處理
   {
     bullet.draw()
     bullet.update()
   }
   
   //怪物的顯示(monster)
   for(let monster of monsters){ //只要是陣列的方式，都可以利用此方式處理
    if(monster.dead == true && monster.deadStartTime>4 ){
      monsters.splice(monsters.indexOf(monster),1)
    }
     monster.draw()
     monster.update()
     for(let bullet of bullets){ //檢查每一個物件
      if(monster.isMonsterInRanger(bullet.p.x,bullet.p.y) ){ //飛彈物件有沒有接觸現在的ball
        // monsters.splice(monsters.indexOf(monster),1) //從倉庫balls裡取出被滑鼠按到的物件編號(balls.indexOf(ball),1)，只取一個
        bullets.splice(bullets.indexOf(bullet),1)         
        score = score + 2 
        monster_sound.play()
        monster.dead = true
      }
    }
   }

   
 
  push()
    fill(255)
    textSize(50)
    text(score,50,50)//在座標(50,50)上，顯示score分數內容
  pop()

  push()  //開始設定
     let dx = mouseX - width/2 //滑鼠
     let dy = mouseY - height/2 //滑鼠
     let angle = atan2(dy,dx) //跟著滑鼠移動
        translate(shipP.x,shipP.y)
        noStroke()
        rotate(angle)
        fill("#cdb4db")
        ellipse(0,0,50)
        fill("#ffafcc")
        triangle(-25,25,-25,-25,50,0) //設定三個點，畫成三角形
  pop()  //設定恢復原樣
  }
  
  
    // function mousePressed(){
    // for(let ball of balls){ //檢查每一個物件
    //   if(ball.isBallInRanger()){ 
    //     balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
    //     score = score + 1
    //   }
    // }
    
    //++++++++++++++按一下產生一個飛彈++++++++++++++++++++++++++++++++++++++
    function mousePressed(){ 
    bullet = new Bullet({}) //在滑鼠按下的地方，產生一個bullet class 元件(產生一個飛彈)
    bullets.push(bullet)    //把bullet的物件放到bullets陣列內
    bullet_sound.play()
  }
    function keyPressed(){
      if(key==" "){ //按下空白鍵
        bullet = new Bullet({}) //在滑鼠按下的地方產生一個新的飛彈(Bullet class)
        bullets.push(bullet)
        bullet_sound.play()
    }
  }
```
#### monster.js
---
```javascript=
var monster_colors = "ede0d4-e6ccb2-ddb892-b08968-7f5539-9c6644".split("-").map(a=>"#"+a)

class Monster {
  constructor(args) {
    this.r = args.r || random(50,100)
    this.p = args.p || createVector(random(0+this.r,width-this.r), random(0+this.r,height-this.r))
    this.v = args.v || createVector(random(-1,1), random(-1,1))
    this.color = args.color || random(monster_colors)
    this.mode = random(["happy","bad"])
    this.dead = false; // 活着
    this.deadStartTime = 0; // 死亡状态开始时间
    this.deadDuration = 8000; // 死亡状态持续时间（以毫秒为单位）
  }
  
  draw() {
    push();
    translate(this.p.x, this.p.y);
    fill(this.color);
    noStroke();
    
    // 绘制星星形状
    beginShape();
    for (var i = 0; i < 25; i++) {
      var angle = map(i, 0, 10, 0, TWO_PI);
      var x = cos(angle) * this.r;
      var y = sin(angle) * this.r;
      vertex(x, y);
      var angle2 = map(i + 0.5, 0, 10, 0, TWO_PI);
      var x2 = cos(angle2) * (this.r / 2);
      var y2 = sin(angle2) * (this.r / 2);
      vertex(x2, y2);
    }
    endShape(CLOSE);
  if (this.dead == false) {
    if (this.mode == "happy") {
      fill(255);
      ellipse(0, 0, this.r/2);
      fill(0);
      ellipse(0, 0, this.r/3);
    } else {
      fill(255);
      arc(0, 0, this.r/2, this.r/2, 0, PI);
      fill(0);
      arc(0, 0, this.r/3, this.r/3, 0, PI);
    }
  } 
  else {
    this.deadStartTime = this.deadStartTime+1
    stroke(0);
    line(-this.r / 2, 0, this.r / 2, 0);
    stroke(this.color);
    strokeWeight(4);
    noFill();
    for (var j = 0; j < 10; j++) {
      rotate(PI / 5);
      line(this.r / 2, 0, this.r, 0);
    }
  }
    pop();
  }

  update() {
    this.p.add(this.v);

    if (this.p.x <= 0 + this.r || this.p.x >= width - this.r) {
      this.v.x = -this.v.x;
    }
    if (this.p.y <= 0 + this.r || this.p.y >= height - this.r) {
      this.v.y = -this.v.y;
    }
  }

isMonsterInRanger(x,y){ //功能:判斷滑鼠按下的位置是否在此物件的範圍內
        let d = dist(x,y,this.p.x,this.p.y) //計算兩點(滑鼠按下與物件中心點)之間的距離，放到d變數內
        if(d<this.r){ //滑鼠與物件的距離小於物件的寬度，代表碰到了
            return true //傳回true的值
        }
        else{ //滑鼠與物件的距離大於物件的寬度，代表沒有碰到
            return false //傳回false值
        }
    }

}
```
#### bullet.js
---
```javascript=

class Bullet{
    constructor(args){ //預設值，基本資料(物件顏色、移動速度、大小、初始顯示位置.......)
        this.r = args.r || 10  //設計飛彈有大有小時，就傳參數，args.r來設定飛彈大小，沒有參數就以10為主
        this.p = args.p ||createVector(width/2,height/2)    //建立一個向量{x:width/2, y:height/2}
        this.v = args.v ||createVector(mouseX-width/2,mouseY-height/2).limit(10)
        this.color = args.color || "#e4c1f9"

    }
    draw(){ //繪出物件
        push()
             translate(this.p.x,this.p.y)
             fill(this.color)
             noStroke()
            ellipse(0,0,this.r)
        pop()
    }
    update(){ //計算出移動後的位置
        this.p.add(this.v)
    }

}
```

#### obj.js
---
```javascript=
class Obj{ //宣告一個類別，針對一個畫的圖案
  constructor(args){ //預設值，基本資料(物件的顏色，移動速度，大小，初始位置......)
    // this.p = args.p || { x:random(0,width), y:random(0,height) } //描述為該物件的初始位置，||(or)，當產生一個物件時，有傳位置參數的話使用該參數，若沒有傳參數就以||後面的設定產出
    this.p = args.p || createVector(random(0,width),random(0,height)) //效果等同上面那行，把原本的{x:..., y:...}改成"向量"方式呈現

    // this.v = { x:random(-1,1), y:random(-1,1) } //描述為該物件的移速
    this.v = createVector(random(-1,1),random(-1,1)) //效果等同上面那行，把原本的{x:..., y:...}改成"向量"方式呈現

    this.size = random(5,10) //描述為該物件的放大倍率
    this.color = random(fill_colors) //充滿顏色
    this.stroke = random(line_colors) //外框線條顏色
  }

  draw(){ //畫出單一個物件形狀
    push() //執行後，依照以下設定
      translate(this.p.x,this.p.y) //以讓物件位置為原點
      scale(this.v.x<0?-1:1,-1) //如果this.v.x<0條件成立，則為1，若不成立，則為-1；代表往右走的圖形象鼻向右，向左的則象鼻向左
      fill(this.color)
      stroke(this.stroke)
      strokeWeight(4)
      beginShape()
        for(var k=0;k<points.length;k=k+1){
          // line(points[k][0]*this.size,points[k][1]*this.size,points[k+1][0]*this.size,points[k+1][1]*this.size)
          // vertex(points[k][0]*this.size,points[k][1]*this.size) //只要設定一個點，當指令到endShape()，會把所有點連在一起，要把上面迴圈points.length-1的-1留著
          curveVertex(points[k][0]*this.size,points[k][1]*this.size) //畫圖為圓弧方式畫，要把上面迴圈points.length-1的-1刪除
        }
      endShape()
    pop() //執行後，回到原始的設定
  }

  update(){ //圖形的移動
    // this.p.x = this.p.x + this.v.x //現在的位置(x)加上現在的速度(x)
    // this.p.y = this.p.y + this.v.y //現在的位置(y)加上現在的速度(y)
    this.p.add(this.v) //設定好向量後才能使用(CreateVector)，可以取代上面兩行指令，效果不變
    //向量sub==>減號

    //知道滑鼠的位置，並建立一個滑鼠的向量
    // let mouseV = createVector(mouseX,mouseY) //把滑鼠的位置轉換成一個向量值
    // let delta = mouseV.sub(this.p).limit(this.v.mag()*1.5) //sub計算滑鼠所在位置向量(mouseV)到物件向量(this.p)的距離，limit(this.v.mag())意思為每次距離縮短(慢慢移動)，mag意思為取得大小，*1.5為速度加快幾倍
    // this.p.add(delta)

    if(this.p.x<=0 || this.p.x>=width){ //x軸碰到左邊(<=0)或者碰到右邊(x>=width)
      this.v.x = -this.v.x //把x軸的速度方向改變
    }
    if(this.p.y<=0 || this.p.y>=height){ //y軸碰到左邊(<=0)或者碰到右邊(x>=width)
      this.v.y = -this.v.y //把y軸的速度方向改變
    }
  }

  isBallInRanger(x,y){ //功能:判斷滑鼠按下的位置是否在此物件的範圍內
    let d = dist(x,y,this.p.x,this.p.y) //計算兩點(滑鼠按下與物件中心點)之間的距離，放到d變數內
    if(d<13*this.size){ //滑鼠與物件的距離小於物件的寬度，代表碰到了
      return true //傳回true的值
    }else{ //滑鼠與物件的距離大於物件的寬度，代表沒有碰到
      return false //傳回false值
    }
  }
}
```
![](https://hackmd.io/_uploads/HJAPr34I3.gif)

---
# 分數>=15會出現:恭喜你，你是神射手，分數<-5，則會出現:再接再厲
### sketch.js
---
```javascript=
let points = [[2, 4], [3,6], [6, 5],[8,6],[9,6],[7,4],[8,4],[8,3],[9 ,3],[7,1],[6,-6],[3,-6],[4,-3],[-3,-3],
[-4,-6],[-7,-6], [-6,-1], [-7, 5],[-6,7],[-4,7],[-5,5],[-4,2], [2, 2],[3,3],[2,3],[4,4],[3,5]]; //小狗
var fill_colors = "ffcdb2-ffb4a2-e5989b-b5838d-6d6875".split("-").map(a=>"#"+a) //填滿顏色
var line_colors = "22223b-4a4e69-9a8c98-c9ada7-f2e9e4".split("-").map(a=>"#"+a) //線條顏色

 //++++++++++設定畫points所有"點"的物件變數
  var ball 
  var balls=[]
  //++++++++++++++++設定飛彈物件變數
  var bullet
  var bullets =[]
  //++++++++++++++++設定怪物的物件變數
  //設定怪物的物件變數
  var monster //把目前要處理的物件，暫存到bullet變數內
  var monsters = [] //把產生的"所有"物件，為物件的倉庫，所有的物件資料都在此
  var score =0 //分數
  var shipP//設定砲台位移

  function preload(){ //加入音樂
    cat_sound = loadSound("mousic/cat3b.mp3")
    bullet_sound = loadSound("mousic/jump13.mp3")
    monster_sound = loadSound("mousic/destruction1.mp3")
  }


  function setup() {
    createCanvas(windowWidth, windowHeight);
    shipP = createVector(width/2,height/2)
    for(var i=0;i<20;i=i+1){ 
      ball = new Obj({}) //產生一個Obj class元件
      balls.push(ball) //把ball的物件放入到balls陣列內
    }
    for(var i=0;i<10;i=i+1){
      monster = new Monster({}) //產生一個Obj class元件
      monsters.push(monster) //把ball的物件放入到balls陣列內
    }
  }
  
 
  function draw() {
    background(220);
  //  for(var j=0;j<balls.length;j=j+1){
  //   ball =balls[j]
  //   ball.draw()
  //   ball.update()
  //  }

  if(keyIsPressed){
    if(key=="ArrowRight" || key=="d"){ //下往右鍵或d往右移動
      shipP.x = shipP.x+5
    }
  
    if(key=="ArrowLeft" || key=="a"){ //按往左鍵或a往左移動0
      shipP.x = shipP.x-5
    }
  
    if(key=="ArrowUp" || key=="w"){ //按往上鍵或w往上移動
      shipP.y = shipP.y-5
    }
  
    if(key=="ArrowDown" || key=="s"){ //按往下鍵或s往下移動
      shipP.y = shipP.y+5
    }

  }


  //貓咪顯示
   for(let ball of balls) //只要是陣列方式，都可以利用此方式處理
   {
     ball.draw()
     ball.update()
     for(let bullet of bullets){ 
        if(ball.isBallInRanger(bullet.p.x,bullet.p.y)){   //物件有無接觸現在的ball 
          balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
          bullets.splice(bullets.indexOf(bullet),1) 
          score = score - 1
          cat_sound.play()
        }
      }
   }
 
  //飛彈顯示
   for(let bullet of bullets) //只要是陣列方式，都可以利用此方式處理
   {
     bullet.draw()
     bullet.update()
   }
   
   //怪物的顯示(monster)
   for(let monster of monsters){ //只要是陣列的方式，都可以利用此方式處理
    if(monster.dead == true && monster.deadStartTime>4 ){
      monsters.splice(monsters.indexOf(monster),1)
    }
     monster.draw()
     monster.update()
     for(let bullet of bullets){ //檢查每一個物件
      if(monster.isMonsterInRanger(bullet.p.x,bullet.p.y) ){ //飛彈物件有沒有接觸現在的ball
        // monsters.splice(monsters.indexOf(monster),1) //從倉庫balls裡取出被滑鼠按到的物件編號(balls.indexOf(ball),1)，只取一個
        bullets.splice(bullets.indexOf(bullet),1)         
        score = score + 2 
        monster_sound.play()
        monster.dead = true
      }
    }
   }
  
  push()
    fill(255)
    textSize(50)
    text(score,50,50)//在座標(50,50)上，顯示score分數內容
  pop()



  
  push()  //開始設定
     let dx = mouseX - width/2 //滑鼠
     let dy = mouseY - height/2 //滑鼠
     let angle = atan2(dy,dx) //跟著滑鼠移動
        translate(shipP.x,shipP.y)
        noStroke()
        rotate(angle)
        fill("#cdb4db")
        ellipse(0,0,50)
        fill("#ffafcc")
        triangle(-25,25,-25,-25,50,0) //設定三個點，畫成三角形
  pop()  //設定恢復原樣

    if (score >= 15) {
      background("#ffcdb2");
      fill(255);
      textSize(100);
      textAlign(CENTER, CENTER);
      text("恭喜你，你是神射手", width / 2, height / 2);
    } else if (score < -5) {
      background("#e5989b");
      fill(255);
      textSize(100);
      textAlign(CENTER, CENTER);
      text("可惜，再接再厲", width / 2, height / 2);
    }
  }

  
  
    // function mousePressed(){
    // for(let ball of balls){ //檢查每一個物件
    //   if(ball.isBallInRanger()){ 
    //     balls.splice(balls.indexOf(ball),1) //按物件，少一個物件
    //     score = score + 1
    //   }
    // }  

    //++++++++++++++按一下產生一個飛彈++++++++++++++++++++++++++++++++++++++
    function mousePressed(){ 
    bullet = new Bullet({}) //在滑鼠按下的地方，產生一個bullet class 元件(產生一個飛彈)
    bullets.push(bullet)    //把bullet的物件放到bullets陣列內
    bullet_sound.play()
  }
    function keyPressed(){
      if(key==" "){ //按下空白鍵
        bullet = new Bullet({}) //在滑鼠按下的地方產生一個新的飛彈(Bullet class)
        bullets.push(bullet)
        bullet_sound.play()
    }
  }
  
