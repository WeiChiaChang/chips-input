<template>
  <div class="chip-container">
    <div
      class="chip"
      v-for="(chip, i) of chips"
      :key="chip.label"
    >
      <div class="chip-wrapper">
        <Editable
          class="chip__content"
          :content="chip"
          @update="updateChip(chip, i, $event)"
        />
        <i class="material-icons" @click="deleteChip(i)">clear</i>
      </div>
      <span class="semicolon">;</span>
    </div>
    <input
      class="current-input"
      v-model="currentInput"
      @keypress.enter="saveChip"
      @keydown.delete="backspaceDelete"
    />
  </div>
</template>

<script>
import Editable from './Editable.vue';
export default {
  name: "ChipsInput",
  components: {
    Editable,
  },
  data() {
    return {
      chips: [],
      currentInput: "",
    };
  },
  methods: {
    updateChip(chip, index, $event) {
      chip = $event;
      this.$set(this.chips, index, $event);
    },
    saveChip() {
      const { chips, currentInput } = this;
      (chips.indexOf(currentInput) === -1) &&
        chips.push(currentInput);
      this.currentInput = "";
    },
    deleteChip(index) {
      this.chips.splice(index, 1);
    },
    backspaceDelete({ which }) {
      which === 8 &&
        this.currentInput === "" &&
        this.chips.splice(this.chips.length - 1);
    },
  },
}
</script>

<style lang="scss" scoped>
.chip-container {
  width: 400px;
  padding: 4px;
  border: 1px solid #ccc;
  min-height: 34px;
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;

  .chip {
    margin: 4px 0;
    padding: 0px 4px;
    display: flex;
    align-items: center;
    height: 24px;
    .chip-wrapper {
      display: flex;
      align-items: center;
      &:hover {
        border-bottom: 1px solid #ccc;
      }
    }
    .chip__content {
      outline: none;
      -webkit-appearance: none;
      border: 0 solid transparent;
      background: transparent;
      padding: 0;
    }
    i {
      cursor: pointer;
      opacity: 0.56;
      margin-left: 8px;
    }
    .semicolon {
      color: #ccc;
      margin: 0 5px;
    }
  }
  .current-input {
    // flex: 1 1 auto;
    width: 3rem;
    height: 24px;
    border: none;
    outline: none;
    padding: 4px 4px 0 4px;
    border-bottom: 1px solid #ccc;
    &:hover {
      border-bottom: 1px solid #ccc;
    }
  }
}
</style>
