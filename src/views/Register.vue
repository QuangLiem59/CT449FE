<template>
    <div class="page">
        <h4>Đăng ký</h4>
        <form @submit.prevent="handleRegister">
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
            <p v-if="successMessage" class="text-success">{{ successMessage }}</p>
            <button type="submit" class="btn btn-success">Đăng ký</button>
            <router-link :to="{ name: 'login' }" class="ml-3">
                Đã có tài khoản? Đăng nhập
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
            successMessage: "",
        };
    },
    methods: {
        async handleRegister() {
            try {
                await AuthService.register({
                    username: this.username,
                    password: this.password,
                });
                this.successMessage = "Đăng ký thành công! Đang chuyển đến trang đăng nhập...";
                setTimeout(() => {
                    this.$router.push({ name: "login" });
                }, 1500);
            } catch (error) {
                this.errorMessage = "Đăng ký thất bại. Tên đăng nhập có thể đã tồn tại.";
            }
        },
    },
};
</script>
