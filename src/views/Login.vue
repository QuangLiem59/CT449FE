<template>
    <div class="page">
        <h4>Đăng nhập</h4>
        <form @submit.prevent="handleLogin">
            <div class="form-group">
                <label>Tên đăng nhập</label>
                <input
                    type="text"
                    class="form-control"
                    v-model="username"
                    required
                />
            </div>
            <div class="form-group">
                <label>Mật khẩu</label>
                <input
                    type="password"
                    class="form-control"
                    v-model="password"
                    required
                />
            </div>
            <p v-if="errorMessage" class="text-danger">{{ errorMessage }}</p>
            <button type="submit" class="btn btn-primary">Đăng nhập</button>
            <router-link :to="{ name: 'register' }" class="ml-3">
                Chưa có tài khoản? Đăng ký
            </router-link>
        </form>
    </div>
</template>

<script>
import AuthService from "@/services/auth.service";

export default {
    data() {
        return {
            username: "",
            password: "",
            errorMessage: "",
        };
    },
    methods: {
        async handleLogin() {
            try {
                const response = await AuthService.login({
                    username: this.username,
                    password: this.password,
                });
                const token = response.token || response.accessToken;
                localStorage.setItem("token", token);
                localStorage.setItem("username", this.username);
                this.$router.push({ name: "contactbook" });
            } catch (error) {
                this.errorMessage = "Tên đăng nhập hoặc mật khẩu không đúng.";
            }
        },
    },
};
</script>
