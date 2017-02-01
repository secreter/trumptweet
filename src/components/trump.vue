<template>
  <div id="canvas-wrap">
    <canvas  id="trump" :width="canvas.width" :height="canvas.height"></canvas>
  </div>
</template>

<script>
export default {
  data () {
    return {
    	canvas:{
    		content:'我怕三十晚上的祝福太多，你会看不到我的问候，我怕初一的鞭炮太吵，你会听不到我的祝福，我怕初二的菜肴太香，你会看不到我的短信，所以选择现在给你送来新年祝福，祝你新春愉快，万事如意！提前给您和家人拜个早年，祝您全家幸福美满。 恭喜发财。羊年行大运，睡觉睡到自然醒，数钱数到手抽筋。'
    	}
    }
  },
  watch: {
    content(){
      this.make()
    }
  },
  created(){
	this.canvas.width=window.innerWidth
	this.canvas.height=window.innerHeight-100
	
  },
  
  props: ['content'],
  methods:{
    make(){
      let 
          w=this.canvas.width,h=this.canvas.height,headH,that=this
      let c=document.getElementById("trump")
      let ctx=c.getContext("2d")
      let headimg=new Image()
      let footimg=new Image()
      // headimg.src='http://og7lnhyuz.bkt.clouddn.com/item/image/jpg/trumphead.jpghead.jpg'
      headimg.src='http://item.redream.cn/trumptweet/head.jpg'
      headimg.crossOrigin = ''; 
      footimg.crossOrigin = ''; 
      headimg.onload=function(){

        
          footimg.src='http://og7lnhyuz.bkt.clouddn.com/item/image/jpg/trumpfoot.jpgfoot.jpg'
          footimg.onload=function(){
            headH=headimg.height/headimg.width*w
            ctx.drawImage(headimg,0,0,w,headH)
            that.writeTxt(c,25,headH,headimg,footimg)
          }
        
      }
      
    },
    //
    writeTxt(canvas,initx,inity,headimg,footimg){
      var maxWidth = this.canvas.width-50;//最宽500像素，否则换行
      var linemargin = 5;
      var lineheight = 20;
      let w=this.canvas.width,h=this.canvas.height,
      headH=headimg.height/headimg.width*w,
      footH=footimg.height/footimg.width*w
        var txt = this.content
        var context = canvas.getContext('2d');
        context.font="20px Arial"
        //自动换行逻辑
        var insertTextData = [];
        var i,x = 0 ,y = 0,linesize = 1;//初始位置
        for(i = 0 ; i<txt.length;i++){
          var currentWord = txt.charAt(i);
          var nextWord = txt.charAt(i + 1) || '';
          // if (currentWord == ' ') continue;
          var currentWidth = context.measureText(currentWord).width;
          var nextWidth = context.measureText(nextWord).width;
          if(x + nextWidth >= maxWidth || currentWord == '\n'){
            x = 0;
            linesize ++;
          }
          y = (lineheight + linemargin) * linesize;
          insertTextData.push({
            text:currentWord,
            x:x,
            y:y
          });
          x = x + currentWidth;
        }
        //计算出高度
        canvas.height = inity+y+20+ lineheight*2 +footH;
        context.clearRect(0,0,maxWidth,y);
        context.fillStyle="#ffffff";
        context.fillRect(0,0,w,canvas.height);
        context.drawImage(headimg,0,0,w,headH)
        context.drawImage(footimg,0,inity+y+20+ lineheight*2,w,footH)
        context.fillStyle="#333333";
        context.font="20px Arial"

        for(i = 0;i<insertTextData.length;i++){
          var item = insertTextData[i];
          context.fillText(item.text,initx+item.x,inity+item.y);
          var lastTxtY=inity+item.y+lineheight*2
        }
        context.fillStyle="#abb4bb";
        context.font="18px Arial"
        context.fillText(this.getTime(),20,lastTxtY);
        context.save();
    },
    getTime(){
      var date = new Date();
      var str=date.getFullYear()+'/'+(1+date.getMonth())+'/'+date.getDate()+ '  '+date.getHours()+':'+date.getMinutes()+':'+date.getSeconds()+'   来自南开一梦'
      return str
    },
    
  }
}
</script>

<style >
	#trump{
    display: none;
    background: #fff;
  }
</style>
