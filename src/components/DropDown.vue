<template>
  <div class="row">
    <div
      class="bar-drop"
      :class="{ active: isDropDown }"
      @click="handleDropdown"
    >
      <span>Chọn tỉnh thành</span>
      <svg
        width="8"
        height="4"
        viewBox="0 0 8 4"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path d="M8 0H0L4 4L8 0Z" fill="#666666" />
      </svg>
    </div>
    <div v-if="isDropDown" class="options">
      <ul>
        <li class="list-item" v-for="province in provinces" :key="province.id">
          <label :for="province.id" @click="handleSelected">
            <input
              :id="province.id"
              type="checkbox"
              :value="province"
              v-model="selectedProvince"
            />
            <img
              class="list-item__uncheckedmarkimg"
              src="../assets/img/uncheckedmark.png"
              alt="unchecked"
            />
            <img
              class="list-item__checkedmarkimg"
              src="../assets/img/checkedmark.png"
              alt="checked"
            />
            <span>
              {{ province.name }}
            </span>
          </label>
        </li>
      </ul>
      <div class="btns">
        <button
          :class="{ btn__active: isBtnActive }"
          class="btn-noActive"
          @click="handleAccept"
        >
          Đồng ý
        </button>
        <button class="btn-close" @click="handleClose">Huỷ</button>
      </div>
    </div>
    <div class="slected" v-if="isDisplay">
      <div
        class="item_select"
        v-for="province in acceptedProvince"
        :key="province.id"
      >
        <span>{{ province.name }}</span>
        <span class="icon-close" @click="handleDelete(province.id)"
          ><CloseOutlined
        /></span>
      </div>
    </div>
  </div>
</template>


<script>
import { CloseOutlined } from "@ant-design/icons-vue";
export default {
  components: {
    CloseOutlined,
  },
  props: {
    provinces: Array,
  },

  name: "DropDown",
  data() {
    return {
      selectedProvince: [],
      acceptedProvince: [],
      currentProvice: [],
      isDropDown: false,
      isBtnActive: false,
      isDisplay: false,
    };
  },
  watch: {
    acceptedProvince(arr) {
      if (arr.length > 0) {
        this.isBtnActive = true;
        this.isDisplay = true;
      } else {
        this.isBtnActive = false;
        this.isDisplay = false;
      }
    },
  },
  methods: {
    handleDropdown() {
      this.isDropDown = !this.isDropDown;
      if (this.currentProvice.length === this.acceptedProvince.length) {
        this.isBtnActive = false;
      }
    },
    handleSelected() {
      setTimeout(() => {
        this.acceptedProvince = [...this.selectedProvince];
      }, 200);
    },
    handleAccept() {
      this.currentProvice = this.selectedProvince;
      this.isDropDown = !this.isDropDown;
    },
    handleClose() {
      this.isDropDown = false;
    },
    handleDelete(id) {
      const index = this.selectedProvince.findIndex(
        (province) => province.id === id
      );
      this.selectedProvince.splice(index, 1);
      this.acceptedProvince = [...this.selectedProvince];
    },
  },
};
</script>
<style>
.row {
  width: 450px;
}
.bar-drop {
  display: flex;
  color: #999999;
  justify-content: space-between;
  align-items: center;
  border: 1.4px solid #999999;
  border-radius: 5px;
  padding: 10px 10px;
}
.active {
  border-color: #58a5d3;
  box-shadow: 0px 0px 8px rgba(120, 120, 120, 0.2);
}
.options {
  box-shadow: 0px 1px 8px rgba(120, 120, 120, 0.2);
  border-radius: 5px;
  padding: 0px 10px;
  padding-top: 15px;
}
.list-item {
  padding: 5px 0px;
  list-style: none;
}
.list-item label {
  display: flex;
  align-items: center;
}
input[type="checkbox"] {
  appearance: none;
}
input[type="checkbox"]:checked ~ .list-item__checkedmarkimg {
  display: block;
}

input[type="checkbox"]:checked ~ .list-item__uncheckedmarkimg {
  display: none;
}
.list-item__checkedmarkimg {
  display: none;
}
.btns {
  padding: 20px 0px;
}
.btn-close {
  color: #067ec4;
  border: none;
  background-color: #fff;
  margin-left: 1.5rem;
}
.btn-noActive {
  border: none;
  background-color: #dcdcdc;
  color: white;
  padding: 7px 19px;
  border-radius: 4px;
}
.btn__active {
  border: none;
  background-color: #007bc3;
  color: white;
  padding: 7px 19px;
  border-radius: 4px;
}

.slected {
  border: 1.4px solid #999999;
  padding: 5px 10px;
  border-radius: 5px;
  margin-top: 20px;
  display: flex;
  gap: 6px;
}
.item_select {
  border: none;
  border-radius: 1000px;
  background-color: #f8f8f8;
  padding: 7px;
}
.icon-close {
  margin-left: 10px;
}
</style>