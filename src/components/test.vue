<template>
  <div class="container">
    <div class="users">
      <el-avatar :size="45">
        <img src="./images/avatar2.jpg">
      </el-avatar>
      <span>User1</span>
      <el-button class="user-btn" type="warning">This</el-button>
    </div>
    <hr>
    <div class="users">
      <el-avatar :size="45">
        <img src="./images/comm2.jpg">
      </el-avatar>
      <span>User2</span>
      <el-button class="user-btn" type="primary">Go to</el-button>
    </div>
  </div>
</template>

<script>
</script>

<style scoped>
.user-btn{
  width: 70px;
  margin-left: 520px;
}
.users span{
  margin-left: 10px;
  font-weight: 700;
  font-family: Plus Jakarta Sans;
}
hr{
  margin: 0;
}
.users:nth-child(1){
  margin-top: -23px;
}
.users{
  display: flex;
  align-items: center;
  transition: all 0.4s;
  margin: 0;
  padding: 10px;
  cursor: pointer;
}
.users:hover{
  background-color: #eeeeee;
}
.container{
  padding: 0 300px;
}
</style>
