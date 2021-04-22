<template>
  <div class="ChipsInput">
    <div
      class="ChipsInput__chipWrapper"
      v-for="(chip) of chips"
      :key="chip.id"
    >
      <div class="ChipsInput__contentWrapper">
        <Editable
          class="ChipsInput__content"
          :content="chip.value"
          @update="updateChip(chip.id, $event)"
        />
        <i class="ChipsInput__deleteIcon material-icons" @click="deleteChip(chip.id)">clear</i>
      </div>
      <span class="ChipsInput__semicolon">;</span>
    </div>
    <input
      class="ChipsInput__currentInput"
      v-model="currentInput"
      @keypress.enter="saveChip"
      @keydown.delete="backspaceDelete"
      @blur="saveChip"
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
    updateChip(id, $event) {
      if ($event === '') {
        const chipIndex = this.chips.findIndex(i => i.id === id);
        this.$delete(this.chips, chipIndex);
      } else {
        const chip = this.chips.find(i => i.id === id);
        this.$set(chip, 'value', $event);
      }
    },
    saveChip() {
      const { chips, currentInput } = this;
      const chipsContent = chips.map(i => i.value);
      if (
        chipsContent.indexOf(currentInput) === -1 &&
        currentInput !== ''
      ) {
        chips.push({
          id: Math.random().toString(36).substr(2, 9),
          value: currentInput
        });
      }
      this.currentInput = "";
    },
    deleteChip(id) {
      const chipIndex = this.chips.findIndex(i => i.id === id);
      this.chips.splice(chipIndex, 1);
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
.ChipsInput {
  width: 400px;
  padding: 4px;
  border: 1px solid #ccc;
  min-height: 34px;
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
  &__chipWrapper {
    margin: 4px 0;
    padding: 0px 4px;
    display: flex;
    align-items: center;
    height: 24px;
  }
  &__contentWrapper {
    display: flex;
    align-items: center;
    &:hover {
      border-bottom: 1px solid #ccc;
    }
  }
  &__content {
    outline: none;
    -webkit-appearance: none;
    border: 0 solid transparent;
    background: transparent;
    padding: 0;
  }
  &__deleteIcon {
    cursor: pointer;
    opacity: 0.56;
    margin-left: 8px;
  }
  &__semicolon {
    color: #ccc;
    margin: 0 5px;
  }
  &__currentInput {
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
