<template>
  <div class="container main-profile">
    <el-row gutter="30">
      <el-col :span="12">
        <el-avatar class="profile-avatar" :size="100">
          <img src="./images/avatar2.jpg">
        </el-avatar>
        <h1 class="user-name">User1</h1>
        <p class="profile-email">@emailname</p>
        <p class="followings"><span>0</span> following</p>
        <p class="followings"><span>10</span> followers</p>
        <p class="profile-info">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus, aperiam consequuntur cumque maxime molestiae natus necessitatibus possimus sapiente.</p>
        <div class="d-flex align-items-center profile-socials mt-4">
          <span><a href="https://instagram.com"><i class="fa-brands fa-instagram"></i></a></span>
          <span><a href="https://twitter.com"><i class="fa-brands fa-twitter"></i></a></span>
          <span><a href="https://tiktok.com"><i class="fa-brands fa-tiktok"></i></a></span>
          <span><a href="https://youtube.com"><i class="fa-brands fa-youtube"></i></a></span>
        </div>
        <div class="d-flex align-items-center mt-4 profile-buttons">
          <el-button type="primary" class="edit-btn">Edit</el-button>
          <el-button class="share-btn">Share</el-button>
          <el-button class="more-btn">...</el-button>
        </div>
      </el-col>
      <el-col :span="12" class="latest-post-zone">
        <img class="latest-post" src="./images/photo_2024-02-08_17-52-47.jpg" alt="latest_post"/>
        <p v-if="photos.length != 0" class="latest-post-name">{{photos[0].title}}</p>
        <div class="about-latest-post">
          <p><span><i class="fa-solid fa-play"></i></span>867</p>
          <p><span><i class="fa-solid fa-heart"></i></span>12</p>
          <p><span><i class="fa-solid fa-comment"></i></span>{{comments.length}}</p>
        </div>
      </el-col>
    </el-row>
    <div class="menu-tab-pane">
      <el-tabs v-model="activeMenu">
        <el-tab-pane label="All" name="all" class="tab-pane-all">
          <img v-for="item in 5" class="posts" src="./images/photo_2024-02-08_17-52-47.jpg">
        </el-tab-pane>
        <el-tab-pane label="Videos" name="videos"></el-tab-pane>
        <el-tab-pane label="Photos" name="photos">
          <img v-for="item in 5" class="posts" src="./images/photo_2024-02-08_17-52-47.jpg">
        </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      activeMenu: 'all'
    }
  },
  props: {
    likeCount: Number,
    comments: Array,
    photos: Array,
  }
}

</script>

<style>
.posts{
  width: 250px;
  margin-right: 3px;
}
.latest-post-name{
  font-size: 22px;
  font-weight: 500;
  margin-top: 15px;
}
.about-latest-post p span{
  margin-right: 10px;
}
.about-latest-post p{
  display: inline-block;
  margin: 0 30px 0 2px;
  color: #495664;
}
.about-latest-post{
  margin-top: 20px;
  display: flex;
}
.latest-post-zone{
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  align-items: center;
}
.latest-post{
  width: 100%;
  height: 340px;
  display: block;
}
.edit-btn{
  width: 90px;
  height: 40px;
  border-radius: 20px;
  border: none;
  font-weight: 700;
}
.share-btn{
  width: 90px;
  height: 40px;
  border-radius: 20px;
  font-weight: 700;
  color: #121417;
  border: 1px solid #9b9b9b;
}
.more-btn{
  border: none;
  height: 40px;
  font-size: 30px;
  color: #9b9b9b;
  font-family: sans-serif;
  display: flex;
  padding-bottom: 22px;

}
.profile-socials span a{
  color: #121417;
}
.profile-socials span i{
  font-size: 18px;
}
.profile-socials span{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  margin-right: 30px;
  border-radius: 50%;
  border: 1px solid #e5e5e5;
  cursor: pointer;
}
.profile-info{
  color: #565759;
  width: 80%
}
.followings span{
  font-weight: 900;
  cursor: pointer;
}
.followings{
  display: inline-block;
  margin-right: 50px;
  font-weight: 500;
  cursor: context-menu;
}
.profile-email{
  color: #A0A0A5;
}
.profile-avatar{
  translate: -20px;
}
.user-name{
  margin-top: 10px;
  font-size: 30px;
  font-weight: 700;
}
.main-profile{
  padding-top: 50px;
  font-family: Plus Jakarta Sans;
}
.menu-tab-pane .el-tabs{
  margin-left: 0;
  margin-top: 100px;
}
.menu-tab-pane .el-tabs .el-tabs__nav-wrap{
  width: 222px;
}
.menu-tab-pane .el-tabs .el-tabs__content{
  margin-top: -14px;
}
</style>
