<script>
import SvgIcon from '@jamescoyle/vue-icon';
import { mdiCardSearchOutline } from '@mdi/js';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

export default {
  props: {
    modelValue: { type: String, default: "" },
  },
  emits: ["submit", "update:modelValue"],
  methods: {
    updateModelValue(e) {
      this.$emit("update:modelValue", e.target.value);
    },
    submit() {
      this.$emit("submit");
    },
  },

  name: "my-component",
  components: {
    SvgIcon
  },
  data() {
    return {
       path: mdiCardSearchOutline,
    }
  }
};

</script>
<template>
  <div class="input-group">
    <input
      type="text"
      class="form-control"
      placeholder="Nhập thông tin cần tìm"
      :value="modelValue"
      @input="updateModelValue"
      @keyup.enter="submit"
    />
    <div class="mx-2 nput-group-append">
      <button class="btn btn-outline-secondary" type="button" @click="submit">
        <!-- <i class="fa-brands fa-searchengin"></i> -->
        <svg-icon type="mdi" :path="path"></svg-icon>
        <font-awesome-icon :icon="['fas', 'magnifying-glass']" />
      </button>
    </div>
  </div>
</template>
