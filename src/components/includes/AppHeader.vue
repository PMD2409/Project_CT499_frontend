<script>
import InputSearch from "@/components/includes/InputSearch.vue";
import DocGiaLog from "@/views/docgia/DocGiaLog.vue";
import NhanVienLog from "@/views/nhanvien/NhanVienLog.vue";
import { ref } from "vue";

export default {
  components: {
    InputSearch,
    NhanVienLog,
    DocGiaLog
  },
  data() {
    return {
      isLoggedIn: false,
      isLoggedInDocGia: false,
    };
  },
  created() {
    const docgia = JSON.parse(sessionStorage.getItem("docgia"));
    const nhanvien = JSON.parse(sessionStorage.getItem("nhanvien"));
    if (nhanvien) {
      this.isLoggedIn = true;
    }
    if (docgia) {
      this.isLoggedInDocGia = true;
    }
  },
  methods: {
    async logout() {
      sessionStorage.removeItem("nhanvien");
      sessionStorage.removeItem("docgia");
      await this.$router.push({ name: "nhanvien.login" });

      if (this.isLoggedIn) {
        alert("Đăng xuất thành công");
        this.isLoggedIn = false;
      }
      if (this.isLoggedInDocGia) {
        alert("Đăng xuất thành công");
        this.isLoggedInDocGia = false;
      }
      window.location.reload();
    },
  },
  setup() {
    const nhanvien = ref(JSON.parse(sessionStorage.getItem("nhanvien")));
    const docgia = ref(JSON.parse(sessionStorage.getItem("docgia")));
    return { nhanvien, docgia };
  },
};
</script>

<style scoped>
#nav {
  background-color: #f8f9fa;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  padding: 10px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.navbar-nav {
  display: flex;
  justify-content: flex-end;
}

.navbar-nav .dropdown {
  margin-right: 10px;
}

.nav-item {
  margin-right: 15px;
}

.nav-link {
  color: #2c3e50;
  padding: 10px 15px;
  border-radius: 5px;
  transition: background-color 0.3s ease;
  font-size: 1rem;
}

.nav-link:hover {
  color: #007bff;
  font-weight: bold;
}

.navbar-brand {
  font-size: 1.5rem;
  font-weight: bold;
  color: #2c3e50;
}

.btn-secondary {
  background-color: #6c757d;
  border: none;
  transition: background-color 0.3s ease, transform 0.2s ease;
}

.btn-secondary:hover {
  background-color: #5a6268;
  transform: scale(1.05);
}

.dropdown-menu {
  background-color: #f8f9fa;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}

.dropdown-item:hover {
  background-color: #e9ecef;
  color: #007bff;
}

.navbar-toggler {
  border: none;
}

.navbar-toggler-icon {
  color: #2c3e50;
}

.navbar-collapse {
  justify-content: space-between;
}

.nav-item {
  margin-right: 10px;
}

body {
  margin: 0;
  padding: 0;
  width: 100%;
  overflow-x: hidden;
}
</style>

<template>
  <div id="app">
    <main>
      <nav class="navbar navbar-expand-lg navbar-light" id="nav">
        <div class="container-fluid">
          <!-- Hiển thị trạng thái đăng nhập -->
          <a v-if="isLoggedIn" href="/Book" class="navbar-brand">
            Quản lý: {{ nhanvien.hoTenNhanVien }}
          </a>
          <a v-if="isLoggedInDocGia" href="#" class="navbar-brand">
            Xin chào: {{ docgia.tenDocGia }}
          </a>
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarText"
            aria-controls="navbarText"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarText">
            <!-- Mục điều hướng -->
            <ul class="navbar-nav me-auto">
              <li v-if="isLoggedIn" class="nav-item active">
                <router-link :to="{ name: 'book' }" class="nav-link">
                  📚 Sách
                </router-link>
              </li>
              <li v-if="isLoggedInDocGia" class="nav-item">
                <router-link :to="{ name: 'sachmuon' }" class="nav-link">
                  📖 Sách mượn
                </router-link>
              </li>
              <li v-if="isLoggedInDocGia" class="nav-item">
                <router-link :to="{ name: 'sachdamuon' }" class="nav-link">
                  ✅ Sách đã mượn
                </router-link>
              </li>
              <li v-if="isLoggedIn" class="nav-item">
                <router-link :to="{ name: 'showdocgia' }" class="nav-link">
                  🧑‍🤝‍🧑 Độc giả
                </router-link>
              </li>
              <li v-if="isLoggedIn" class="nav-item">
                <router-link :to="{ name: 'shownxb' }" class="nav-link">
                  🏢 Nhà xuất bản
                </router-link>
              </li>
              <li v-if="isLoggedIn" class="nav-item">
                <router-link :to="{ name: 'quanlysachmuon' }" class="nav-link">
                  📋 Quản lý sách mượn
                </router-link>
              </li>
              <!-- Dropdown Nhân viên -->
              <div class="dropdown" v-if="!isLoggedIn && !isLoggedInDocGia">
                <button class="btn btn-secondary dropdown-toggle" type="button" id="dropdownMenuButton1" data-bs-toggle="dropdown" aria-expanded="false">
                  Nhân Viên
                </button>
                <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
                  <li>
                    <router-link :to="{ name: 'nhanvien.register' }" class="nav-link dropdown-item">
                      ➕ Đăng Ký Quản Lý
                    </router-link>
                  </li>
                  <li>
                    <router-link :to="{ name: 'nhanvien.login' }" class="nav-link dropdown-item">
                      🔑 Đăng Nhập Quản Lý
                    </router-link>
                  </li>
                </ul>
              </div>

              <!-- Dropdown Độc giả -->
              <div class="dropdown" v-if="!isLoggedIn && !isLoggedInDocGia">
                <button
                  class="btn btn-secondary dropdown-toggle"
                  type="button"
                  id="dropdownMenuButton2"
                  data-bs-toggle="dropdown"
                  aria-expanded="False"
                >
                  Độc Giả
                </button>
                <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton2">
                  <li class="nav-item">
                    <router-link :to="{ name: 'docgia.register' }" class="nav-link">
                      ➕ Đăng Ký  Độc Giả
                    </router-link>
                  </li>
                  <li class="nav-item">
                    <router-link :to="{ name: 'docgia.login' }" class="nav-link">
                      🔑 Đăng Nhập Độc Giả
                    </router-link>
                  </li>
                </ul>
              </div>
            </ul>
            <!-- Dropdown Đăng xuất -->
            <ul class="navbar-nav ms-auto">
              <li v-if="isLoggedIn || isLoggedInDocGia" class="nav-item">
                <router-link
                  :to="{ name: 'nhanvien.login' }"
                  @click="logout"
                  class="nav-link"
                >
                  🚪 Đăng xuất
                </router-link>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </main>
  </div>
</template>
