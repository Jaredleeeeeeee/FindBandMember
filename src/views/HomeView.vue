

<template>
  <main>
    <Home />

    <div class="container">
      <div class="img"></div>
      <div class="content">
        <h1>找不到人玩樂團嗎？</h1>
        <RouterLink to="/information" class="infobtn">了解更多</RouterLink>
      </div>
    </div>
  </main>
</template>
<style scoped>
  .container {
    background-color: #000;
    display: flex;
    width: 100%;
    height: 800px;
  }

  .img {
    background-image: url(../assets/instrumentphoto.jpg);
    background-position: top;
    background-repeat: no-repeat;
    background-size: cover;
    width: 50%;
  }

  .content {
    width: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 20px;
  }

  .content h1 {
    color: #D1603D;
  }

  .infobtn {
    text-decoration: none;
    color: #fff;
    background-color: #d1603df1;
    font-weight: 400;
    border-radius: 20px;
    padding: 15px;
    margin-left: 15px;
  }

  .infobtn:hover {
    background-color: #D1603D;
    color: #2f2f2f;
    font-weight: 500;
    font-size: 25px;

  }


</style>
