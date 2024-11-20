<template>
    <div v-if="muonSach">
    <h1 class="text-start mx-3">Mượn sách</h1>
    <MuonSachForm
        
        :muonSach="muonSach"
        @submit:muonSach="addMuonSach"
    />
        <p>{{ message }}</p>
    </div>
</template>
<script>
import MuonSachForm from "@/components/muonsach/MuonSachForm.vue";
import BookService from "@/services/book.service";
import MuonSachService from "@/services/muonsach.service";
export default {
    components: {
        MuonSachForm,
    },
    props: {
        id: { type: String, required: true },
    },
    data() {
        return {
            muonSach: null,
            message: "",
        };
    },
    methods: {
        async addMuonSach(data) {
            try {
                await MuonSachService.create(data);
                alert('Mượn sách thành công')
                setTimeout(() => {
                    this.$router.push("/sachdamuon");
                }, 1000);
            } catch (error) {
                console.log(error);
            }
        },
        async getBook(id) {
            try {
                this.muonSach = await BookService.get(id);
            } catch (error) {
                console.log(error);
                this.$router.push({
                    name: "notfound",
                    params: {
                        pathMatch: this.$route.path.split("/").slice(1),
                    },
                    query: this.$route.query,
                    hash: this.$route.hash,
                });
            }
        },
        
        
    },
    created() {
        this.getBook(this.$route.params.id);
    },
};
</script>