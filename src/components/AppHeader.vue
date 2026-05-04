<template>
    <nav class="navbar navbar-expand navbar-dark bg-dark">
        <a href="/" class="navbar-brand">Ứng dụng Quản lý danh bạ</a>
        <div class="mr-auto navbar-nav">
            <li class="nav-item">
                <router-link :to="{ name: 'contactbook' }" class="nav-link">
                    Danh bạ
                    <i class="fas fa-address-book"></i>
                </router-link>
            </li>
        </div>
        <div class="navbar-nav ml-auto">
            <template v-if="username">
                <span class="nav-link text-light">
                    <i class="fas fa-user"></i> {{ username }}
                </span>
                <button class="btn btn-outline-light btn-sm ml-2" @click="logout">
                    <i class="fas fa-sign-out-alt"></i> Đăng xuất
                </button>
            </template>
            <template v-else>
                <router-link :to="{ name: 'login' }" class="nav-link">Đăng nhập</router-link>
                <router-link :to="{ name: 'register' }" class="nav-link">Đăng ký</router-link>
            </template>
        </div>
    </nav>
</template>

<script>
export default {
    computed: {
        username() {
            return localStorage.getItem("username");
        },
    },
    methods: {
        logout() {
            localStorage.removeItem("token");
            localStorage.removeItem("username");
            this.$router.push({ name: "login" });
        },
    },
};
</script>
