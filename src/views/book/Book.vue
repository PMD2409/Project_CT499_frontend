<script>
import BookCard from '@/components/book/BookCard.vue';
import BookList from '@/components/book/BookList.vue';
import InputSearch from '@/components/includes/InputSearch.vue';
import BookService from '@/services/book.service';
export default {
    components: {
        InputSearch,
        BookCard,
        BookList
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
        bookStrings(){
            return this.Sach.map((sach) => {
                const { tenSach, maSach, tacGia, namXuatBan, soQuyen, donGia } = sach;
                return [tenSach, maSach, tacGia, namXuatBan, soQuyen, donGia].join(" ");
            });
        },  
        filteredBooks() {
            if (!this.searchText) {
                return this.Sach;
            }
            return this.Sach.filter((_sach,index) => {
                return this.bookStrings[index].toLowerCase().includes(this.searchText.toLowerCase());
            });
        },
        activeBook() {
            if (this.activeIndex <0) {
                return null;
            }
            return this.filteredBooks[this.activeIndex];
        },
        filteredBooksCount() {
            return this.filteredBooks.length;
        },
    },
    methods:{
        async retrieveBook(){
            try {
                this.Sach = await BookService.getAll();
            } catch (error) {
                console.error(error);
            }
        },
        refreshList(){
            this.retrieveBook();
            this.activeIndex = -1;
        },
        goToAddBook(){
            this.$router.push({ name: "book.add" });
        },
    },
    mounted(){
        this.refreshList();
    },
};
</script>
<style scoped>
.page {
    text-align: left;
    margin: 20px auto;
    max-width: 1200px;
}

form {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

.row {
    margin: 0 -10px;
}

.col-md-9, .col-md-3 {
    padding: 10px;
}

button {
    font-size: 16px;
    padding: 10px 20px;
    border-radius: 5px;
    transition: background-color 0.3s ease, transform 0.2s ease;
}

button:hover {
    background-color: #0056b3; /* Biến đổi màu nhấn */
    transform: scale(1.05);  /* Hiệu ứng hover */
}

button.btn-outline.btn-primary {
    color: #0056b3;
    border-color: #0056b3;
}

button.btn-outline.btn-primary:hover {
    background-color: #0056b3;
    color: white;
}

button.btn-outline.btn-success {
    color: #28a745;
    border-color: #28a745;
}

button.btn-outline.btn-success:hover {
    background-color: #28a745;
    color: white;
}

p {
    color: #6c757d;
    font-style: italic;
}

h4 {
    font-weight: bold;
    margin-bottom: 15px;
}

.badge-warning {
    color: #856404;
    background-color: #ffc107;
    cursor: pointer;
}

.badge-warning:hover {
    background-color: #e0a800;
}
</style>

<template>
   <div class="page">
    <form class="d-flex w-50">
    <InputSearch v-model="searchText" placeholder="Tìm kiếm sách..." />
</form>
<div class="row">
    <div class="mt-3 col-md-9">
        <h4>Tất cả sách</h4>
        <p v-if="filteredBooksCount > 0">
            Có {{ filteredBooksCount }} sách được tìm thấy.
        </p>
        <BookList
            v-if="filteredBooksCount > 0"
            :Sach="filteredBooks"
            v-model:activeIndex="activeIndex"
        />
        <p v-else>Không có sách nào phù hợp.</p>
        <div class="mt-3 row justify-content-around align-items-center">
            <button class="btn col-md-4 mb-2 mt-3 btn-outline btn-primary" @click="refreshList()">
                Làm mới
            </button>
            <button class="btn btn-outline col-md-4 mb-2 btn-success mt-3" @click="goToAddBook">
                <i class="fas fa-plus"></i> Thêm mới
            </button>
        </div>
    </div>
    <div class="mt-3 col-md-3">
        <div v-if="activeBook">
            <h4>Chi tiết</h4>
            <BookCard :Sach="activeBook" />
            <router-link
                :to="{ name: 'book.edit', params: { id: activeBook._id } }"
            >
                <span class="mt-2 badge badge-warning bg-warning mb-2 pb-2">
                    <i class="fas fa-edit"></i> Hiệu chỉnh
                </span>
            </router-link>
        </div>
    </div>
</div>
  </div>
</template>