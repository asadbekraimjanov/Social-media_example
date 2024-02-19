<template>
  <div  class="main-like-page">
    <div class="container d-flex justify-content-center align-items-center flex-wrap">
      <div>
        <el-avatar class="likes-avatar-me"><img src="./images/avatar2.jpg"></el-avatar>
      </div>
      <div class="about-user">
        <p>User1</p>
        <span>{{users.length}} followers</span>
      </div>
      <el-button @click="clickUser" class="vw-profile-btn" type="info">View profile</el-button>

      <div class="count-comment">
        {{comments.length}} comments
      </div>
      <div style="width: 900px">
        <app-home-comments v-for="(item, num) in comments" :num="num" :comments="comments"></app-home-comments>
      </div>
    </div>
  </div>
</template>

<script>
import appHomeComments from "@/components/AppHomeComments.vue";
export default {
  data(){
    return {
    }
  },
  components: {
    'app-home-comments': appHomeComments
  },
  props: {
    comments: Array,
    users: Array,
    loading: Boolean,
    clickUser: Function
  }
}
</script>

<style>
.loader{
  display: none;
}
.vw-profile-btn{
  margin-right: 20px;
}
.count-comment{
  width: 100%;
  padding: 20px 210px;
  font-family: Plus Jakarta Sans;
  font-size: 18px;
  font-weight: 700;
  line-height: 23px;
  letter-spacing: -0.27px;

}
.about-user span{
  font-family: Plus Jakarta Sans;
  font-size: 14px;
  font-weight: 400;
  line-height: 21px;
  letter-spacing: 0px;
  color: #637587;
}
.about-user p{
  margin: 0;
  width: 690px;
  font-family: Plus Jakarta Sans;
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  letter-spacing: 0px;
  color: #121417;
}
.about-user{
  margin: 0;
  margin-left: 20px;
}
.likes-avatar-me{
  width: 60px;
  height: 60px;
}
.main-like-page{
  margin-top: 100px;
}
</style>
