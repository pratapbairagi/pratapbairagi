<!DOCTYPE html>
<html>

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title></title>
    <style>
    *{
      box-sizing: border-box;
      padding: none;
      margin: none;
    }
    
    body{
      width: 100%;
      height: 100vh;
    }
     #bar{
     width: 250px;
     height: 190px;
     border-radius: 2%;
     background: transparent;
     border: 3px solid aqua;
     }
     
     #bar2{
     width: 350px;
     height: 266px;
     border-radius: 2%;
     background: transparent;
     border: 3px solid aqua;
     }
    
      #video{
        display: block;
        width: 100%;
        height: 100%;
        border-radius: 1%;
        position: relative;
      }
      
      #control{
        width: 100%;
        height: 20%;
        background: green;
        position: relative;
        float:center;
        flex-direction: row;
        justify-content: space-around;
        align-items: center;
        margin-top: -13.7%;
        display: none;
      }
      
      .btn{
      width: 8%;
      height: 8%;
      font-size: 50%;
      line-height: 8%;
      position: relative;
      border: transparent;
      background: transparent;
      padding: 0;
      cursor: pointer;
      display: block;
      }
 
      #progress{
        width: 30%;
        height: 4%;
        position: relative;
        background: red;
        margin-left: -2%;
      } 
      progress[type=change]::-webkit-progress-bar{
        -webkit-appearance: none;
        background: gold;
        border-radius: 8px;
      }
      progress[type=change]::-webkit-progress-value{
        -webkit-appearance: none;
        background: red;
      }
      #time{
        position: relative;
        width: 5%;
        height: 4%;
        line-height: 8%;
        font-size: 35%;
        font-weight: bold;
        color: white;
        margin: 0 3%;
      }
      
      
      input[type=range]{
        -webkit-appearance: none;
        background: linear-gradient(to right,brown,red,orangered,orange,yellow,lightyellow,yellow,lightgreen,green);
        height: 3%;
        line-height: 3%;
        width: 20%;
        border-radius: 10px;
        margin-left: 5%;
      }
      input[type=range]::-webkit-slider-thumb{
        -webkit-appearance: none;
        width: 6px;
        height: 6px;
        border-radius: 50%;
        background: black;
        box-shadow: -30% 0px 0.6% dimgrey;
      }
      .leftTime {
      position:relative;
      width: 5%;
      height: 4%;
      line-height: 14%;
      font-weight: bold;
      color: white;
      font-size: 28%;
      margin: 0 2%;
      }
      .volNo{
        width: 5%;
        height: 4%;
        line-height: 10%;
        font-size: 30%;
        color: white;
      }
   /*   #vol{
        position: relative;
        height: 3%;
        width: 25%;
      }*/
      
     #bar:hover #control{
        display: block;
        
        width: 100%;
        height: 40px;
        background: transparent;
        position: relative;
        display: flex;
        flex-direction: row;
        justify-content: space-around;
        align-items: center;
      }
      .mute{
        background: transparent;
        border: none;
        padding: none;
        width: 8%;
        height: 8%;
        line-height: 8%;
        font-size: 50%;
      }
      circle{
        cx:50;
        cy:50;
        r:10;
        fill: transparent;
        stroke-width: 2;
        stroke: red;
        stroke-dasharray:62.26,62.26;
        margin-left: -10%;
      }
      .circle{
        animation-name: pratap;
        animation-timing-function: linear;
     animation-iteration-count:infinite;
      }
      svg{
        margin: 0 -12%;
      }
      
      @keyframes pratap{
      0%{
        stroke-dashoffset: 0;
      }
      25%{
      stroke-dashoffset: 15.565;
      }
      50%{
      stroke-dashoffset: 31.13;
      }
      675%{
      stroke-dashoffset: 46.695;
      }
      100%{
      stroke-dashoffset: 62.26;
      }
    }
     
      
    </style>
</head>

<body>
   <div id="bar">
  <video id="video" src="Baatein_Kuch_Ankahee_Si-Unplugged_-_Life_in_a_Metro|Kangna,Shilpa|Suhail_Kaul|Pritam(144p).mp4"></video>
    
    <div id="control">
      
      <button class="btn">▶️</button>
   
   <div id="time">Run</div>
   
   <progress id="progress"
   value="" min="0" max="100" type="change"></progress>
   
    <div class="leftTime">Remain</div>
   
   <!-- prog animation -->
   <svg style="width: 100px; height: 100px; background: transparent;">
     <circle class="circle circle1"></circle>
   </svg>
   
     <input type="range" name="" id="vol" value="0.50" min="0"
  max="1.00" step="0.01" onchange="volFun()"/>
  
  <div class="volNo"></div>
  
  <button class="mute">🎶</button>
      
    </div>
    
    
  
  <script>
  var play=document.querySelector(".btn");
  var video=document.querySelector('#video');
  var progress=document.querySelector('#progress');
  var time=document.querySelector('#time');
  var left=document.querySelector('.leftTime');
  var cir=document.querySelector('.circle');
  
  
    play.addEventListener('click',function(){
      if(video.paused){
        video.play();
        cir.style.animationDuration=video.duration+'s';
       cir.style.animationPlayState='play';
       play.innerHTML='⏸️';
      }else{
        video.pause();
        cir.style.animationPlayState='paused';
        cir.style.animationDuration=video.duration+'s';
        
        play.innerHTML='▶️';
      }
    });
    
    video.addEventListener('play',pro);
    function pro(){
     setInterval(function(){
        //math for usint mathematical calculation and abs() and round() is for roundup the video
        progress.value=Math.round((video.currentTime / video.duration)*100);
        //for show the video running time
       time.innerHTML=Math.round(video.currentTime)+'s';
       left.innerHTML=Math.round(video.duration-video.currentTime);
     });
    }
    
    //for volume slide
    var vol=document.querySelector('#vol');
    var volNo=document.querySelector('.volNo');
    function volFun(){
      video.volume=vol.value;
      
      volNo.innerHTML=video.volume*100+'%';
    }
    
    //funtion for mute
    var mute=document.querySelector('.mute');
    mute.addEventListener('click',muteFun);
    function muteFun(){
      if(video.muted){
        video.muted=false;
        mute.innerHTML='🎶';
      }else{
        video.muted=true;
        mute.innerHTML='🔇'
      }
    }
/*    //for change progress
    progress.addEventListener('mouseup touchend', progChange);
    function progChange(e){
      var newProg=video.getDuration()*(e.target.value/100);
      video.progress(newProg);
    }
    
    
    //for screen change
    var bar=document.querySelector('#bar');
    function screen(){
      if(video.paused || video.play){
        bar.classList.replace('bar','bar2');
      }else{
        bar.classList.replace('bar2','bar');
      }
    }
  */
  
  </script>

</body>

</html>
