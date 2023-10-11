<script setup lang="ts">
import { ref, computed } from "vue";

const numOfPeople = ref<number>(1);
const priceOfBill = ref<number>(0);
const tipPercentage = ref<number>(5);

const tipAmountPerPerson = computed(() => {
  return (
    ((priceOfBill.value / 100) * tipPercentage.value) /
    numOfPeople.value
  ).toFixed(2);
});

const totalTipAmount = computed(() => {
  return ((priceOfBill.value / 100) * tipPercentage.value).toFixed(2);
});

const resetAllValues = () => {
  numOfPeople.value = 1;
  priceOfBill.value = 0;
  tipPercentage.value = 5;
};
</script>

<template>
  <div class="tip-calculator">
    <form class="tip-calculator__form">
      <div class="tip-calculator__input-container">
        <label>Bill</label>
        <input v-model.number="priceOfBill" placeholder="€" type="number" />
      </div>
      <div class="tip-calulator__input-container">
        <span>Fill in Tip %</span>
        <input
          v-model.number="tipPercentage"
          placeholder="Tip percentage"
          type="number"
        />
        <span v-if="tipPercentage < 5" class="tip-calculator__error">
          Fill in a minimun percentage of 5%
        </span>
      </div>
      <div className="tip-calculator__input-container">
        <div className="tip-calculator__label-container">
          <label>Number of people</label>
        </div>
        <input
          v-model.number="numOfPeople"
          placeholder="Number of people"
          type="number"
        />
        <span v-if="numOfPeople < 1" class="tip-calculator__error"
          >Value can't be zero</span
        >
      </div>
    </form>

    <div class="tip-calculator__checkout">
      <div class="tip-calculator__checkout-container">
        <div class="tip-calculator__checkout-info">
          <span class="tip-calculator__total">Tip Amount</span>
          <span class="tip-calculator__person">/ person</span>
        </div>
        <div class="tip-calculator__tip-amount">
          <h2>€ {{ tipAmountPerPerson }}</h2>
        </div>
      </div>
      <div class="tip-calculator__checkout-container">
        <div>
          <span class="tip-calculator__total">Total</span>
          <span class="tip-calculator__person">/ person</span>
        </div>
        <div class="tip-calculator__tip-amount">
          <h2>€ {{ totalTipAmount }}</h2>
        </div>
      </div>
      <button @click="resetAllValues" class="tip-calculator__reset-btn">
        Reset
      </button>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@import "assets/styles/variables";

.tip-calculator {
  display: flex;
  align-items: center;
  justify-content: center;
  background: white;
  padding: 50px;
  border-radius: 20px;
  gap: 40px;

  @media #{$media-mobile} {
    display: block;
  }

  &__input-container {
    display: flex;
    flex-direction: column;
    margin: 20px 0;
  }

  &__error {
    color: red !important;
  }

  &__label-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  input {
    padding: 10px 20px;
    width: 100%;
    box-sizing: border-box;
  }

  label,
  span,
  p {
    display: block;
    text-align: left;
    margin: 0;
  }

  &__checkout {
    display: block;
    justify-content: space-between;
    align-items: center;
    background: hsl(183, 100%, 15%);
    color: white;
    padding: 50px;
    border-radius: 20px;
    width: 250px;

    &-container {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    h2 {
      color: hsl(172, 67%, 45%);
    }
  }

  &__total {
    color: white;
  }

  &__person {
    text-align: left;
    color: hsl(184, 14%, 56%);
  }

  &__reset-btn {
    display: block;
    width: 100%;
    background-color: hsl(172, 67%, 45%);
    margin-top: 50px;

    &:hover {
      background-color: hsl(189, 41%, 97%);
    }
  }
}
</style>
