<script>
import BookCard from "@/components/book/BookCard.vue";
import BookList from "@/components/book/BookList.vue";
import InputSearch from "@/components/includes/InputSearch.vue";
import BookService from "@/services/book.service";
export default {
  components: {
    InputSearch,
    BookCard,
    BookList,
  },
  data() {
    return {
      Sach: [],
      searchText: "",
      activeIndex: -1,
    };
  },
  watch: {
    searchText() {
      this.activeIndex = -1;
    },
  },
  computed: {
    bookStrings() {
      return this.Sach.map((sach) => {
        const { tenSach, maSach, tacGia, namXuatBan, soQuyen, donGia } = sach;
        return [tenSach, maSach, tacGia, namXuatBan, soQuyen, donGia].join(" ");
      });
    },
    filteredBooks() {
      if (!this.searchText) {
        return this.Sach;
      }
      return this.Sach.filter((_sach, index) => {
        return this.bookStrings[index]
          .toLowerCase()
          .includes(this.searchText.toLowerCase());
      });
    },
    activeBook() {
      if (this.activeIndex < 0) {
        return null;
      }
      return this.filteredBooks[this.activeIndex];
    },
    filteredBooksCount() {
      return this.filteredBooks.length;
    },
  },
  methods: {
    async retrieveBook() {
      try {
        this.Sach = await BookService.getAll();
      } catch (error) {
        console.error(error);
      }
    },
    refreshList() {
      this.retrieveBook();
      this.activeIndex = -1;
    },
  },
  mounted() {
    this.refreshList();
  },
};
</script>
<style scoped>
.page {
  text-align: left;
  /* max-width: 750px; */
  padding: 2rem;
}
</style>
<template>
  <div class="page ">
    <form class="d-flex w-50">
      <InputSearch v-model="searchText" />
    </form>
    <div class="row">
    <div class="mt-3 col-md-9">
      <h4>Tất cả sách</h4>
      <BookList
        v-if="filteredBooksCount > 0"
        :Sach="filteredBooks"
        v-model:activeIndex="activeIndex"
      />
      <p v-else>Không có sách nào nào.</p>
      <div class="mt-3 row mx-1 align-items-center">
        <button
          class="btn col-md-4 mb-2 mt-3 btn-outline btn-primary"
          @click="refreshList()"
        >
          Làm mới
        </button>
      </div>
    </div>
    <div class="col-md-3 mt-3">
      <div v-if="activeBook">
        <h4>Chi Tiết Sách</h4>
        <BookCard :Sach="activeBook" />
        <router-link
          :to="{ name: 'sachmuon.add' ,params:{id: activeBook._id}}"
          class="btn btn-success my-3 col-md-4 mb-2 mt-3 mx-2"
        >
          Mượn Sách
        </router-link>
      </div>
    </div>
  </div>
  </div>
</template>
