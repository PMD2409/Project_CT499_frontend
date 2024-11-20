<script>
export default {
  props: {
    Sach: { type: Array, default: [] },
    activeIndex: { type: Number, default: -1 },
  },
  emits: ["update:activeIndex"],
  methods: {
    updateActiveIndex(index) {
      this.$emit("update:activeIndex", index);
    },
  },
};
</script>
<template>
  <div class="row">
  <div class="card col-md-2 my-1 mx-1" v-for="(sach, index) in Sach" :key="sach._id"
      :class="{ active: index === activeIndex }">
    <img src="../../assets/book.png"
      @click="updateActiveIndex(index)"  class="card-img-top" alt="...">
    <div class="card-body">
      <h5 class="card-title">
        {{ sach.tenSach }}
      </h5>
      <p class="card-subtitle mb-2 text-muted">
        {{ sach.tacGia}}
      </p>
    </div>
  </div>
  </div>
</template>
