<template>
  <div>
    <h1>Đăng Nhập Nhân Viên</h1>
    
    <form @submit="login">
      
      <label class="form-label" for="username"></label>
      <input
        class="form-control m-auto w-25"
        type="text"
        id="username"
        v-model="hoTenNhanVien"
        placeholder="Username"
        required
      />
      <label class="form-label mt-2" for="password"></label>
      <input
        class="form-control w-25 m-auto"
        type="password"
        id="password"
        v-model="password"
        placeholder="Password"
        required
      />
      <button class="btn btn-primary my-2" type="submit">Login</button>
    </form>
  </div>
</template>
<script>
import axios from "axios";
// import { toast } from 'vue3-toastify';
// import 'vue3-toastify/dist/index.css';
export default {
  data() {
    return {
      hoTenNhanVien: "",
      password: "",
      success: null,
      error: null,
    };
  },
  methods: {
    login(event) {
      event.preventDefault();
      axios
        .post("/api/nhanvien/login", {
          hoTenNhanVien: this.hoTenNhanVien,
          password: this.password,
        })
        .then(async (response) => {
          const nhanvien = response.data;
          // toast.success("Đăng nhập thành công", {
          //   timeout: 1000,
          // });
          sessionStorage.setItem("nhanvien", JSON.stringify(nhanvien));
          await this.$router.push("/Book");
          window.location.reload();
        })
        .catch((error) => {
          alert("Sai mật khẩu hoặc tên đăng nhập");
        });
    },
  },
};
</script>
