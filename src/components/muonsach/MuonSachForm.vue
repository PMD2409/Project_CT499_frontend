<template>
  <div class="row">
    <div class="w-75 mx-3">
      <Form @submit="submitMuonSach" class="w-50">
        <div class="form-group">
          <label class="mb-2" for="maSach">Mã Sách</label>
          <Field
            name="maSach"
            type="text"
            id="maSach"
            class="form-control"
            v-model="muonSachLocal.maSach"
          />
        </div>
        <div class="form-group">
          <label class="mb-2" for="tenSach">Tên sách</label>
          <Field
            name="tenSach"
            type="text"
            id="tenSach"
            class="form-control"
            v-model="muonSachLocal.tenSach"
          />
        </div>
        <div class="form-group">
          <label class="mb-2" for="maDocGia">Mã độc giả</label>
          <Field
            name="maDocGia"
            type="text"
            id="maDocGia"
            class="form-control"
            v-model="muonSachLocal.maDocGia"
          />
        </div>
        <div class="form-group">
          <label class="mb-2" for="tenDocGia">Tên độc giả</label>
          <Field
            name="tenDocGia"
            type="text"
            id="tenDocGia"
            class="form-control"
            v-model="muonSachLocal.tenDocGia"
          />
        </div>
        <div class="form-group">
          <label class="mb-2" for="ngayMuon">Ngày mượn</label>
          <Field
            name="ngayMuon"
            id="ngayMuon"
            type="date"
            class="form-control"
            v-model="muonSachLocal.ngayMuon"
          />
        </div>
        <div class="form-group">
          <label class="mb-2" for="ngayTra">Ngày trả</label>
          <Field
            name="ngayTra"
            id="ngayTra"
            type="date"
            class="form-control"
            v-model="muonSachLocal.ngayTra"
          />
        </div>
        <div class="form-group">
          <label for="trangThai">Trạng thái</label>
          <select id="trangThai" name="trangThai" v-model="muonSachLocal.trangThai">
          <option value="Đã mượn">Đã mượn</option>
          </select>
        </div>
        <button type="submit" class="btn mt-3 btn-primary">Xác nhận</button>
      </Form>
    </div>
  </div>
</template>
<script>
import { Field, Form } from "vee-validate";
export default {
  components: {
    Form,
    Field,
  },
  emits: ["submit:muonSach"],
  props: {
    muonSach: { type: Object, required: true },
  },
  data() {
    return {
      muonSachLocal: this.muonSach,
    };
  },
  methods: {
    submitMuonSach() {
      this.$emit("submit:muonSach", this.muonSachLocal);
    },
  },
};
</script>
<style scoped>
@import "@/assets/form.css";
</style>
