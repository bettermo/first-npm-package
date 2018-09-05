<template>
<div id="app">
   <div class="uploader">
      <p class="title"><i>文件上传</i><span>{{numLProp}}/{{maxImgs}}</span></p>
      <van-uploader :after-read="onRead" :disabled="disabledProp">
         <div class="slotWrap">
            <van-icon name="add2" size="80px" :color="disabledProp?color1:color0" class="iconUp" />
            <!-- <span class="progress">{{percent}}%</span> -->
         </div>
      </van-uploader>
      <div class="imgView">
         <ul class="imgList">
            <li v-for="(item,idx) in images" :key="idx" @click.stop="preview(idx)">
               <van-icon name="clear" class="delImg" @click.stop="delImg(idx)" />
               <img :src="item" />
            </li>
         </ul>
      </div>
      <van-progress :percentage="percent" :show-pivot="false"  v-show="showPercent"/>
   </div>
</div>

</template>
<script>
import { ImagePreview} from "vant";
import '../../assets/reset.less'
export default {
   name: "HelloWorld",
   // props: ["percent","images","maxImgs","Reaffirm","disabled","numL","showPercent"],   
   props: {
      "percent":{
         type:Number,
         default:0
      },
      "images":{
         type:Array,
         default:()=>[]
      },
      "maxImgs":{
         type:Number,         
         default:1
      },
      "disabled":{
         type:Boolean,
         default:false
      },
      "numL":{
         type:Number,         
         default:0
      },
      "showPercent":{
         type:Boolean,         
         default:true
      }
   },
   data() {
      return {
         color0:'#c9ced3',
         color1:'#f5f5f5',
         numLProp:this.numL,
         disabledProp:this.disabled,
      };
   },
   mounted(){
      this.numLProp = this.images.length || 0
   },
   watch: {
    "images": {
      handler(newValue) {
　　　　　　this.whichLarge(newValue.length,this.maxImgs)
　　　　},
　　　　deep: true
    }
   },
   methods: {
      onRead(file) {
         this.$emit("uploadImg", { file: file})     //事件回调
      },
      upload(data) {
         console.log(data);
      },
      delImg(idx) {
         //删除图片
         this.$emit("delImg", { idx: idx})     //事件回调
         
      },
      preview(idx) {
         //预览图片
         ImagePreview({
            images: this.images,
            startPosition: idx || 0
         });
      },

      whichLarge(l,r){
         this.numLProp = l
         if(l >= r){
            this.disabledProp = true
         }else{
            this.disabledProp = false
         }
      },
   }
};
</script>
<style lang="less">

.van-dialog {
   width: 70%;
}
.van-progress {
   height: 2px;
}
.uploader {
   padding: 10px;
   text-align:left;
   .title {
      line-height: 28px;
      font-size: 16px;
      overflow: hidden;
      color: #999;
      i {
         float: left;
         padding-left: 7px;
      }
      span{
         float: right;
      }
   }
   .slotWrap {
      overflow: hidden;
      margin-right: 10px; 
      position: relative;     
      .iconUp {
         position: relative;
         top: 3px;
         width: 80px;
         height: 80px;
      }
      .progress {
         position: absolute;
         bottom: -24px;
         display: inline-block;
         text-align: center;
         line-height: 24px;
         width: 100%;
      }
   }
   .imgView {
      display: inline-block;
      .imgList {
         li {
            float: left;
            width: 80px;
            height: 80px;
            overflow: hidden;
            position: relative;
            background-color: #ccc;
            margin-left: 5px;
            img {
               width: 100%;
               float: left;
            }
            i {
               position: absolute;
               top: 3px;
               right: 3px;
               color: #3d3e3f;
               font-size: 18px;
            }
         }
      }
   }
}
</style>
