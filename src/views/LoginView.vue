<template>
    <div class="container">
        <form @submit.prevent>
            <h3>登入</h3>

            <div class="loginForm">
                <label for="">帳號: </label>
                <input type="email">
            </div>

            <div class="loginForm">
                <label for="">密碼: </label>
                <input type="password">
            </div>

            <button type="submit" class="btn">
                登入
            </button>

            <button class="btn">
                <RouterLink to="/" class="btn">註冊</RouterLink>
            </button>

            <p>
                <RouterLink to="/" class="forget_password">忘記密碼?</RouterLink>
            </p>
        </form>
    </div>
</template>

<script>

</script>

<style lang="scss" scoped>
.container {
    height: 800px;
    width: 100%;
    background-color: rgba(0, 0, 0, .8);
    background-image: url(../assets/glenn-van-de-wiel-DWHSc8o8K9Y-unsplash.jpg);
    background-size: cover;
    background-blend-mode: multiply;
    background-position: center center;
    padding-top: 100px;
}

.container form h3 {
    font-weight: 600;
    font-size: 26px;
    color: #D1603D;
}

form {
    background-color: #39373747;
    width: 80%;
    height: 250px;
    padding: 20px;
    color: #fff;
    margin: auto;
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    border-radius: 15px;
}

.loginForm input {
    width: 100%;
}

.btn {
    background-color: #D1603D;
    color: white;
    padding: 4px 10px;
    margin: 6px 0;
    border: none;
    cursor: pointer;
    width: 50%;
    border-radius: 15px;
    text-decoration: none;
}

.btn:hover {
    opacity: 0.8;
}
form .forget_password {
    color: #D1603D;
    font-size: 15px;
}

@media (min-width: 768px) {

    .container {
        form {
            width: 30%;
        }
    }
}
</style>


