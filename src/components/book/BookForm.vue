<template>
  <Form @submit="submitBook" class="form-container">
    <div class="form-group">
      <label for="maSach">Mã sách</label>
      <Field
        name="maSach"
        type="text"
        class="form-control"
        v-model="bookLocal.maSach"
        placeholder="Nhập mã sách"
      />
    </div>
    <div class="form-group">
      <label for="tenSach">Tên sách</label>
      <Field
        name="tenSach"
        type="text"
        class="form-control"
        v-model="bookLocal.tenSach"
        placeholder="Nhập tên sách"
      />
    </div>
    <div class="form-group">
      <label for="tacGia">Tác giả</label>
      <Field
        name="tacGia"
        type="text"
        class="form-control"
        v-model="bookLocal.tacGia"
        placeholder="Nhập tên tác giả"
      />
    </div>
    <div class="form-group">
      <label for="namXuatBan">Năm xuất bản</label>
      <Field
        name="namXuatBan"
        type="number"
        class="form-control"
        v-model="bookLocal.namXuatBan"
        placeholder="Nhập năm xuất bản"
      />
    </div>
    <div class="form-group">
      <label for="maNXB">Nhà xuất bản</label>
      <Field
        name="maNXB"
        as="select"
        class="form-control"
        v-model="bookLocal.maNXB"
      >
        <option value="" disabled>Chọn nhà xuất bản</option>
        <option v-for="nxb in nxbList" :key="nxb._id" :value="nxb.maNXB">
          {{ nxb.tenNXB }}
        </option>
      </Field>
    </div>
    <div class="form-group">
      <label for="soQuyen">Số quyển</label>
      <Field
        name="soQuyen"
        type="number"
        class="form-control"
        v-model="bookLocal.soQuyen"
        placeholder="Nhập số quyển"
      />
    </div>
    <div class="form-group">
      <label for="donGia">Giá</label>
      <Field
        name="donGia"
        type="number"
        class="form-control"
        v-model="bookLocal.donGia"
        placeholder="Nhập giá"
      />
    </div>
    <div class="form-actions">
      <button class="btn btn-primary"><i class="fas fa-save"></i> Lưu</button>
      <button
        v-if="bookLocal._id"
        type="button"
        class="btn btn-danger"
        @click="deleteBook"
      >
        <i class="fas fa-trash"></i> Xóa
      </button>
    </div>
  </Form>
</template>

<script>
import { Form, Field } from "vee-validate";

export default {
  components: {
    Form,
    Field,
  },
  emits: ["submit:Sach", "delete:Sach"],
  props: {
    Sach: { type: Object, required: true },
    nxbList: { type: Array, required: true }, // Danh sách NXB
  },
  data() {
    return {
      bookLocal: this.Sach,
    };
  },
  methods: {
    submitBook() {
      this.$emit("submit:Sach", this.bookLocal);
    },
    deleteBook() {
      this.$emit("delete:Sach", this.bookLocal._id);
    },
  },
};
</script>

<style scoped>
/* Bố cục form */
.form-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  padding: 20px;
  background: #f8f9fa;
  border: 1px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Trường nhập liệu */
.form-group label {
  font-weight: bold;
  margin-bottom: 5px;
  color: #333;
}

.form-control {
  padding: 10px 15px;
  border-radius: 5px;
  border: 1px solid #ccc;
  font-size: 16px;
  width: 100%;
}

.form-control:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.3);
  outline: none;
}

/* Hành động nút */
.form-actions {
  display: flex;
  justify-content: space-between;
  grid-column: 1 / -1; /* Căn chỉnh cả chiều ngang form */
}

button {
  padding: 12px 20px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  border: none;
  transition: all 0.3s ease;
}

button.btn-primary {
  background-color: #007bff;
  color: white;
}

button.btn-primary:hover {
  background-color: #0056b3;
}

button.btn-danger {
  background-color: #dc3545;
  color: white;
}

button.btn-danger:hover {
  background-color: #c82333;
}

@media (max-width: 576px) {
  .form-actions {
    flex-direction: column;
  }

  button {
    width: 100%;
    margin-bottom: 10px;
  }
}
</style>
