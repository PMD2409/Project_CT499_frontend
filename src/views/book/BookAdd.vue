<template>
    <div v-if="Sach" class="page">
      <h4>Thêm sách</h4>
      <BookForm
        :Sach="Sach"
        @submit:Sach="addBook"
        :nxbList="nxbList"  
      />
      <p>{{ message }}</p>
    </div>
  </template>
  
  <script>
  import BookForm from "@/components/book/BookForm.vue";
  import BookService from "@/services/book.service";
  import NxbService from "@/services/nhaxuatban.service";  // Import NXBService
  
  export default {
    components: {
      BookForm,
    },
  
    data() {
      return {
        Sach: {},
        nxbList: [],  // Danh sách nhà xuất bản
        message: "",
      };
    },
  
    methods: {
      async addBook(data) {
        try {
          await BookService.create(data);
          alert("Thêm mới thành công");
          this.$router.push({ name: "book" });
        } catch (error) {
          console.log(error);
        }
      },
  
      async loadNXBList() {
        try {
          this.nxbList = await NxbService.getAll();  // Lấy danh sách nhà xuất bản từ NXBService
        } catch (error) {
          console.log("Lỗi khi lấy danh sách nhà xuất bản", error);
        }
      },
    },
  
    created() {
      this.loadNXBList();  // Gọi phương thức khi component được tạo
    },
  };
  </script>
  