<template>
  <div class="container m-auto w-100">
    <form @submit="register">
      <section class="vh-100 d-flex align-items-center custom-bg">
        <div class="container py-5">
          <div class="row justify-content-center">
            <div class="col-12 col-lg-8 col-xl-6">
              <div class="card card-registration p-4">
                <div class="card-body">
                  <h3 class="text-center mb-4 title-text">Đăng Ký Độc Giả</h3>

                  <!-- Row 1: Mã độc giả và Mật khẩu -->
                  <div class="row mb-4">
                    <div class="col-md-6 mb-3">
                      <input type="text" id="maDocGia" class="form-control input-field"
                             placeholder="Mã độc giả" v-model="docgiaLocal.maDocGia" required/>
                    </div>
                    <div class="col-md-6 mb-3">
                      <input type="password" id="password" class="form-control input-field"
                             placeholder="Mật khẩu" v-model="docgiaLocal.password" required/>
                    </div>
                  </div>

                  <!-- Row 2: Họ tên -->
                  <div class="row mb-4">
                    <div class="col-md-6 mb-3">
                      <input type="text" id="hoLot" class="form-control input-field"
                             placeholder="Họ" v-model="docgiaLocal.hoLot" required/>
                    </div>
                    <div class="col-md-6 mb-3">
                      <input type="text" id="tenDocGia" class="form-control input-field"
                             placeholder="Tên" v-model="docgiaLocal.tenDocGia" required/>
                    </div>
                  </div>

                  <!-- Row 3: Địa chỉ và Số điện thoại -->
                  <div class="row mb-4">
                    <div class="col-md-6 mb-3">
                      <input type="text" id="diaChi" class="form-control input-field"
                             placeholder="Địa chỉ" v-model="docgiaLocal.diaChi" required/>
                    </div>
                    <div class="col-md-6 mb-3">
                      <input type="text" id="dienThoai" class="form-control input-field"
                             placeholder="Số điện thoại" v-model="docgiaLocal.dienThoai" required/>
                    </div>
                  </div>

                  <!-- Row 4: Ngày sinh và Giới tính -->
                  <div class="row mb-4">
                    <div class="col-md-6 mb-3">
                      <input type="date" id="ngaySinh" class="form-control input-field"
                             placeholder="Ngày sinh" v-model="docgiaLocal.ngaySinh" required/>
                    </div>
                    <div class="col-md-6 mb-3">
                      <input type="text" id="gioiTinh" class="form-control input-field"
                             placeholder="Giới tính" v-model="docgiaLocal.gioiTinh" required/>
                    </div>
                  </div>

                  <!-- Submit Button -->
                  <div class="text-center mt-4">
                    <button type="submit" class="btn btn-primary btn-lg px-5">Đăng ký</button>
                  </div>

                </div>
              </div>
            </div>
          </div>
        </div>
      </section>
    </form>
  </div>
</template>

<script>
export default {
  emits: ['submit:DocGia'],
  props: {
    docGia: {
      type: Object,
      default: () => ({
        maDocGia: '',
        password: '',
        hoLot: '',
        tenDocGia: '',
        ngaySinh: '',
        gioiTinh: '',
        diaChi: '',
        dienThoai: ''
      })
    }
  },
  data() {
    return {
      docgiaLocal: { ...this.docGia }, // Dữ liệu độc giả local
    };
  },
  methods: {
    register(e) {
      e.preventDefault(); // Ngăn chặn reload trang
      this.$emit('submit:DocGia', this.docgiaLocal); // Gửi dữ liệu lên component cha
    }
  }
};
</script>

<style scoped>
/* Hình nền */
.custom-bg {
  background-image: url('C:\Users\ADMIN\Downloads\ct44903_project_quanlymuonsach-master\frontend\src\assets\istockphoto-1358158784-612x612.jpg'); /* Đường dẫn tới hình ảnh của bạn */
  background-size: cover; /* Làm cho ảnh phủ đầy khung */
  background-position: center;
  background-attachment: fixed;
  color: white;
  
  /* Tạo khung và góc tròn */
  border: 5px solid #ffffff; /* Khung trắng */
  border-radius: 20px; /* Góc tròn */
  padding: 15px; /* Khoảng cách giữa ảnh nền và khung */
  overflow: hidden; /* Đảm bảo ảnh không bị tràn ra ngoài góc tròn */
}

/* Tiêu đề */
.title-text {
  font-family: 'Roboto', sans-serif;
  font-weight: 700;
  color: #fff;
  text-transform: uppercase;
}

/* Card (khung đăng ký) */
.card-registration {
  background-color: rgba(255, 255, 255, 0.9); /* Nền trắng nhẹ */
  border-radius: 15px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2); /* Bóng đổ mềm mại */
  animation: fadeIn 1s ease-out;
}

/* Hiệu ứng fade-in cho card */
@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(30px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Input form */
.input-field {
  border: 2px solid #ddd;
  border-radius: 8px;
  padding: 14px;
  transition: all 0.3s ease;
}

.input-field:focus {
  box-shadow: 0 0 10px rgba(81, 203, 238, 1);
  border-color: rgba(81, 203, 238, 1);
  background-color: #f0f8ff;
}

/* Button */
.btn-primary {
  background-color: #2575fc;
  border-color: #2575fc;
  border-radius: 25px;
  font-size: 18px;
  padding: 14px 35px;
  transition: all 0.3s ease;
}

.btn-primary:hover {
  background-color: #1e63cc;
  border-color: #1e63cc;
  transform: scale(1.05);
}

/* Text alignment and spacing */
.text-center {
  text-align: center;
}

.mt-4 {
  margin-top: 2rem;
}

.mb-4 {
  margin-bottom: 2rem;
}

/* Cải thiện spacing và khoảng cách */
.row {
  margin-bottom: 2rem;
}

.card-body {
  padding: 30px;
}

/* Thêm border-radius cho các góc của input và nút bấm */
input.input-field, select.input-field, button {
  border-radius: 8px;
}

/* Responsive Design cho các cột */
@media (max-width: 768px) {
  .card-registration {
    padding: 20px;
  }
  
  .row {
    margin-bottom: 1.5rem;
  }
}
</style>
