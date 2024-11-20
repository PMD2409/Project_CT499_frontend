<template>
  <div class="book-info">
    <div class="book-item">
      <strong class="label">Mã:</strong>
      <span>{{ Sach.maSach }}</span>
    </div>
    <div class="book-item">
      <strong class="label">Tên:</strong>
      <span>{{ Sach.tenSach }}</span>
    </div>
    <div class="book-item">
      <strong class="label">Tác giả:</strong>
      <span>{{ Sach.tacGia }}</span>
    </div>
    <div class="book-item">
      <strong class="label">Năm xuất bản:</strong>
      <span>{{ Sach.namXuatBan }}</span>
    </div>
    <div class="book-item">
      <strong class="label">Nhà xuất bản:</strong>
      <span>{{ Sach.maNXB }}</span>
    </div>
    <div class="book-item">
      <strong class="label">Số quyển:</strong>
      <span>{{ Sach.soQuyen }} quyển</span>
    </div>
    <div class="book-item">
      <strong class="label">Giá:</strong>
      <span>{{ Sach.donGia }} VND</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    Sach: { type: Object, required: true },
  },
};
</script>

<style scoped>
.book-info {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  margin: 20px auto;
}

.book-item {
  display: flex;
  justify-content: space-between;
  margin-bottom: 15px;
  font-size: 16px;
}

.book-item:last-child {
  margin-bottom: 0;
}

.label {
  font-weight: bold;
  color: #333;
}

span {
  color: #555;
}

.book-item:hover {
  background-color: #f1f1f1;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

@media (max-width: 768px) {
  .book-info {
    padding: 15px;
  }

  .book-item {
    font-size: 14px;
  }
}
</style>
