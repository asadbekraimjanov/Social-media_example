<template>
  <div class="container">
    <el-row :gutter="20">
      <el-col :span="12">
        <img v-if="photos.length != 0" class="el-main-image" src="../components/images/photo_2024-02-08_17-52-47.jpg">
        <el-skeleton v-if="photos.length == 0" animated>
          <template #template>
            <el-skeleton-item class="el-main-image" variant="image"/>
          </template>
        </el-skeleton>
      </el-col>
      <el-col :span="12">
        <div v-if="photos.length != 0 && comments.length != 0 && users.length != 0" class="main-info">
          <h1>{{photos[numb].title[0].toUpperCase() + photos[numb].title.slice(1)}}</h1>
          <p>Posted by {{users[numb].email}}</p>
          <el-button class="view-comment-btn" type="primary" v-if="!this.viewComments" @click="vwComments">View comments</el-button>
          <el-button class="view-comment-btn" type="primary" v-if="this.viewComments" @click="vwComments">Close comments</el-button>
        </div>
        <el-skeleton v-if="photos.length == 0" style="margin-top: 100px; margin-left: 35px" :rows="4"/>
      </el-col>
    </el-row>
    <div class="post-info">
      <div class="photo-info">
        <i class="fa-heart" :class="[likePress ? 'fa-solid' : 'fa-regular']" @click="LikeCounter"/>
        <a>{{likeCount}}</a>
        <i @click="vwComments" class="fa-regular fa-comment"></i>
        <a>{{comments.length}}</a>
        <i class="fa-regular fa-paper-plane"></i>
        <a>4</a>
      </div>
    </div>
    <div class="commentaries" v-if="viewComments">
      <el-row>
        <el-col :span="1"><el-button class="arrow-dn-btn p-3" :icon="ArrowDown" @click="showAllComments"></el-button></el-col>
        <el-col :span="23" class="vw-comments-div">
          <p class="vac-p">View all comments</p>
          <span class="vac-span">View all comments</span>
        </el-col>
      </el-row>
      <div>
        <app-home-comments v-for="(item, num) in comNumber" :num="num" :comments="comments"></app-home-comments>
      </div>
      <div>
        <el-row>
          <el-col :span="1">
            <el-avatar><img src="./images/us%20comm.jpg"></el-avatar>
          </el-col>
          <el-col :span="23">
            <el-input
                @keypress.enter="postComment"
                v-model="commentaryInput"
                placeholder="Add a comment"
            ></el-input>
            <el-button class="btn-post" type="primary" @click="postComment">Post</el-button>
          </el-col>
        </el-row>
      </div>
    </div>
  </div>
  <app-profile :likeCount="likeCount"></app-profile>
</template>

<script>
import {ArrowDown} from "@element-plus/icons-vue";
import AppHomeComments from "@/components/AppHomeComments.vue";
import axios from "axios";

export default {
  components: {AppHomeComments},
  computed: {
    ArrowDown() {
      return ArrowDown
    },
    'app-home-comments': AppHomeComments
  },
  data(){
    return{
      viewComments: false,
      likeCount: 12,
      likePress: false,
      commentaryInput: '',
      comNumber: 2,
    }
  },
  props: {
    photos: Array,
    comments: Array,
    numb: Number,
    users: Array,
  },
  methods: {
    postComment(){
      axios.post('https://jsonplaceholder.typicode.com/comments', {
        name: 'User1',
        body: this.commentaryInput,
        email: '@asadbekraimjonov09',
        id: this.comments.length+2,
        postId: this.comments.length+2,
      }).then(rest => {
        this.comments.unshift(rest.data)
        // console.log(this.comments)
        console.log(rest.data)
        // console.log(this.comments)
      }).catch(error => console.log(error))

      this.commentaryInput = ''
    },
    showAllComments(){
      this.comNumber += 8
    },
    vwComments(){
      this.viewComments = !this.viewComments
      this.comNumber = 2
    },
    LikeCounter(){
      if (this.likePress == false){
        this.likePress = !this.likePress
        this.likeCount++
      }
      else {
        this.likePress = !this.likePress
        this.likeCount--
      }
    }
  }
}
</script>

<style>
.photo-info i{
  width: 23px;
}
.photo-info a{
  width: 10px;
}
.btn-post{
  width: 84px;
  height: 32px;
  border-radius: 10px;
  padding: 0px 16px 0px 16px;
  position: absolute;
  margin-left: -90px;
  margin-top: 6px;
}
.el-input__wrapper{
  height: 45px;
  margin-left: 0.5em;
  border-radius: 10px;
  background-color: #F0F2F5;
  font-family: Plus Jakarta Sans;
  font-size: 16px;
  font-weight: 400;
  line-height: 24px;
  letter-spacing: 0px;
}
.photo-info{
  display: flex;
  align-items: center;
  width: 100%;
  height: 60px;
  margin-top: 20px;
  margin-left: 3%;
  font-size: 24px;
  color: #637587;
}
.photo-info a{
  font-family: Plus Jakarta Sans;
  font-size: 13px;
  font-weight: 700;
  line-height: 20px;
  letter-spacing: 0.19499999284744263px;
  padding-left: 10px;
  margin-right: 4%;
}
.photo-info i{
  cursor: pointer;
}
.arrow-dn-btn{
  background-color: #F0F2F5;
  border: none;
  width: 48px;
  height: 48px;
  font-size: 24px;
  font-weight: 900;
  color: #121417;
  border-radius: 10px;
}
.arrow-dn-btn:active{
  background-color: #e1e1e1;
}
.commentaries{
  padding-left: 2.2%;
}
.vw-comments-div{
  height: 28px;
}
.vac-p{
  margin: 0 0 0 1.1em;
  font-family: Plus Jakarta Sans;
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  letter-spacing: 0px;
  color: #121417;
}
.vac-span{
  margin: 0 0 0 1.1em;
  font-family: Plus Jakarta Sans;
  font-size: 14px;
  font-weight: 400;
  line-height: 21px;
  letter-spacing: 0px;
  color: #637587;
}
.comment-name{
  font-family: Plus Jakarta Sans;
  font-size: 14px;
  font-weight: 700;
  line-height: 21px;
  letter-spacing: 0.20999999344348907px;
  color: #121417;
  margin: 0;
}
.comment-name span{
  font-family: Plus Jakarta Sans;
  font-size: 14px;
  font-weight: 400;
  line-height: 21px;
  letter-spacing: 0px;
  color: #637587;
  margin-left: 20px;
}
.commentary{
  font-family: Plus Jakarta Sans;
  font-size: 14px;
  font-weight: 400;
  line-height: 21px;
  letter-spacing: 0px;
  color: #121417;
  margin-bottom: 10px;
}
.fa-thumbs-up{
  font-size: 20px;
  color: #637587;
  cursor: pointer;
}
.comment-box span{
  font-family: Plus Jakarta Sans;
  font-size: 14px;
  font-weight: 400;
  line-height: 21px;
  letter-spacing: 0px;
  color: #637587;
  margin-left: 10px;
}
</style>
