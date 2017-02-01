<template>
  <div id="app">
    <header>
      <img class="head-img" src="./assets/head.jpg" alt="">
      <textarea v-model="content" class="head-input" cols="30" rows="10"></textarea>
      <mt-button @click="popup" class="head-btn" type='primary'>发布</mt-button>
    </header>
    <nav class="nav">
      <mt-button class="nav-btn" @click="hot" type='primary'>热门</mt-button>
      <mt-button class="nav-btn" @click="recommend" type='danger'>精选文案</mt-button>
    </nav>
    <mt-tab-container v-model="active">
      <mt-tab-container-item id="tab-container1">
        <a v-for="item in imgList" :href="item.href"><img class="img-list"  :src="item.url" alt=""></a>
        
      </mt-tab-container-item>
      <mt-tab-container-item id="tab-container2">
        <mt-cell class="txt-list" v-for="txt in recommendData" :title="txt" @click.native="bindContent(txt)"></mt-cell>
      </mt-tab-container-item>
      
    </mt-tab-container>

    <mt-popup
      v-model="popupVisible"
      position="right">
      <trump :content="content"></trump>
      <div class="notice">长按图片保存</div>

    </mt-popup>
    <footer >
      <p>本Tweet纯属事主瞎编，与遵纪守法纯情善良的“南开一梦”公众号无关。</p>
    </footer>
  </div>
</template>

<script>
import trump from './components/trump'

export default {
  name: 'app',
  components: {
    trump
  },
  data(){
    return {
      active:'tab-container1',
      popupVisible:false,
      recommendData:[
        'I am afraid the morning firecrackers too noisy, you will not hear my blessing, I`m afraid the first two days of the dishes too incense, you will see Not see my message. So choose this time to send you a blessing, I wish you and your family Happy New Year, good health. Give you an early worship!',
        '群主发红包，Make 红包 Great Again！',
        '听说爱你的人今晚12点整会发压岁钱给你，Tweet还是要发的，万一实现了呢？',
        '《西游伏妖》有人约不？',
        'China No.1',
        'No class and homework for Chinese students in the Spring Festival. 你想太多了',
        '谁发红包我跟谁好！',
        '▓╄→涐怕彡╈晚sんαɡ甾柷褔冭哆，妳譮看囨椡涐甾問鍭，涐怕初壹甾鞭炮冭ο少，妳譮ロ斤囨椡涐甾柷褔，涐怕初②甾寀餚冭楿，妳譮看囨椡涐甾短信，葰鉯選擇現恠給中國仌送嗰柷褔給大jíα拝嗰早年，柷大jíα荃jíα緈褔羙慲。 恭喜發財。★',
        '我怕三十晚上的祝福太多 ，您会不在意我的问候， 我怕初一早上的鞭炮太吵， 您会听不到我的祝福 ，我怕初二中午的菜肴太香， 您会看不见我的短信。 所以选择现在这个时候给您送来祝福，祝您及你家人新春愉快，身体健康。给您拜个早年!',
        '春节到了，不管你给不给红包，我都会祝你鸡年红红火火;不管你送不送祝福，我都会祝你鸡年五福临门;不管你回不回信息，我都祝你鸡年欢欢喜喜。',
        '有没有敬业福！',
        '你妈逼你结婚了吗？',
        '春节出租男朋友？',
        '春节来了，现在免费帮家长带孩子，有18-26岁的吕孩子可以送到我这里，免费帮各位家长照看。所以男生勿扰，谢谢合作~',

      ],
      imgList:[
        {
          href:'http://item.redream.cn/truthmoment/index.php?id=220043&userid=o6UDkwIppYchG79HknNe-9fuYugQ',
          url:'http://og7lnhyuz.bkt.clouddn.com/item/image/jpg/truth.jpgtruth.jpg'
        },
        {
          href:'',
          url:'http://og7lnhyuz.bkt.clouddn.com/item/image/jpg/jinye.jpgjinye.jpg'
        },
        {
          href:'https://open.weixin.qq.com/connect/oauth2/authorize?appid=wx96bfa7c4e7c79526&redirect_uri=http%3A%2F%2Fitem.redream.cn%2Fpyq%2Ftalk.php&response_type=code&scope=snsapi_userinfo&state=66&from=singlemessage#wechat_redirect ',
          url:'http://og7lnhyuz.bkt.clouddn.com/item/image/jpg/qiaoqiao.jpgword.jpg'
        },
        {
          href:'https://open.weixin.qq.com/connect/oauth2/authorize?appid=wx96bfa7c4e7c79526&redirect_uri=http%3A%2F%2Fitem.redream.cn%2Fpyq%2Ftalk.php&response_type=code&scope=snsapi_userinfo&state=67&from=singlemessage#wechat_redirect ',
          url:'http://og7lnhyuz.bkt.clouddn.com/item/image/jpg/great.jpggreat.jpg'
        },  
      ],
      content:''
    }

  },
  methods:{
    hot(){
      this.active='tab-container1'
    },
    recommend(){
      this.active='tab-container2'
    },
    bindContent(txt){
      this.content=txt
      console.log(txt,1)
    },
    popup(){
      this.popupVisible=true
      this.toImg()
    },
    toImg(){
      var dataurl = document.getElementById('trump').toDataURL('image/jpeg');
      var wrap=document.getElementById('canvas-wrap')
      var imgNode =wrap.getElementsByTagName('img')[0]
      if (imgNode) {
        imgNode.src=dataurl;
        imgNode.style.width="100%";
      }else{
       imgNode=document.createElement("img");
       imgNode.src=dataurl;
       imgNode.style.width="100%";
       wrap.appendChild(imgNode);
      }
      
      
      
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
header{
  background: #eee;
  overflow: hidden;
}
.head-img{
  width: 100%;
}
.head-input{
  border: solid 1px #eee;
  width: 100%;
  font-size: 18px;
  padding: 5px;
}
.head-btn{
  float: right;
  margin:10px 10px;
}
.nav{
  background: #999;
  display: flex;
  justify-content: space-around;
}
.nav-btn{
  width: 50%
}
.img-list{
  width: 100%
}
#tab-container2{
  background: #f8f8f8;
}
.txt-list{
  margin: 10px 0;
  /*padding: 10px 0;*/
}
.notice{
  display: flex;
  background: #eee;
  justify-content: center;
  align-items: center;
  height: 50px;
  width: 100%;
}
footer{
  background: #eee;
  font-size: 16px;
  padding: 20px 10px;
}
footer p{
  text-align: center;
  color: #999;
}
</style>
