<template>
  <div
    :class="[{ active: isActive }, 'dropdown']"
    @click="toggleActive"
    aria-hidden="true"
  >
    <label :for="index">
      <input
        ref="textBox"
        type="text"
        :placeholder="item[0]"
        :id="index"
        readonly
      />
    </label>
    <div class="option">
      <div ref="time" @click="show('time')" aria-hidden="true">
        {{ item[0] }}
      </div>
      <div ref="noDubt" @click="show('noDubt')" aria-hidden="true">
        {{ item[1] }}
      </div>
      <div ref="hurryUp" @click="show('hurryUp')" aria-hidden="true">
        {{ item[2] }}
      </div>
      <div
        ref="sendIt"
        v-if="item[3]"
        @click="show('sendIt')"
        aria-hidden="true"
      >
        {{ item[3] }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Array,
      default: () => [],
    },
    index: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      isActive: false,
    };
  },
  methods: {
    show(anything) {
      switch (anything) {
        case "time":
          this.$refs.textBox.value = this.$refs.time.innerText;
          break;
        case "noDubt":
          this.$refs.textBox.value = this.$refs.noDubt.innerText;
          break;
        case "hurryUp":
          this.$refs.textBox.value = this.$refs.hurryUp.innerText;
          break;
        case "sendIt":
          this.$refs.textBox.value = this.$refs.sendIt.innerText;
          break;
        default:
          this.$refs.textBox.value = "Выберете вариант из списка";
      }
    },
    toggleActive() {
      if (this.isActive === false) {
        this.isActive = true;
      } else this.isActive = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.dropdown {
  position: relative;
  width: 100%;
  height: 50px;
  padding-bottom: 25px;
}

.dropdown::before {
  content: "";
  position: absolute;
  right: 20px;
  top: 17px;
  z-index: 10;
  width: 8px;
  height: 8px;
  border: 2px solid #333;
  border-top: 2px solid #fff;
  border-right: 2px solid #fff;
  transform: rotate(-45deg);
  transition: 0.5s;
  pointer-events: none;
}

.dropdown.active::before {
  top: 22px;
  transform: rotate(-225deg);
}

.dropdown input {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  cursor: pointer;
  background: #fff;
  border: none;
  outline: none;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.05);
  padding: 12px 40px;
  border-radius: 50px;
}

.dropdown .option {
  z-index: 11;
  position: absolute;
  top: 51px;
  width: 100%;
  background: #fff;
  box-shadow: 0 30px 30px rgba(0, 0, 0, 0.05);
  border-radius: 50px;
  overflow: hidden;
  display: none;
}

.dropdown.active .option {
  display: block;
}

.dropdown .option div {
  padding: 12px 20px;
  cursor: pointer;
}

.dropdown .option div:hover {
  background: #62baea;
  color: #fff;
}
</style>
