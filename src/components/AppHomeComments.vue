<template>
  <el-row class="pt-4 pb-4" >
    <el-col :span="1"><el-avatar><img src="./images/comm1.jpg"></el-avatar></el-col>
    <el-col :span="23" >
      <div class="comment-box mx-2" >
        <p class="comment-name">{{comments[num].name}} <span>{{num+2}} days ago</span></p>
        <p class="commentary">{{comments[num].body}}</p>
        <i @click="commentLike" class="fa-regular fa-thumbs-up"></i>
        <span>{{commentLikeCounter}}</span>
      </div>
    </el-col>
  </el-row>
</template>
<script>
export default {
  data(){
    return{
      commentLikeCounter: 0,
    }
  },
  props: {
    comments: Array,
    num: Number,
  },
  methods: {
    commentLike(){
      if (this.commentLikeCounter == 0){
        this.commentLikeCounter = 1
      }
      else this.commentLikeCounter = 0
    }
  }
}
</script>

<style>

</style>
