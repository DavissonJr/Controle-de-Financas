<template>
   <div class="income-item">
    <div class="removeItem"></div>
    <div class="desc">{{ income.desc }}</div>
    <div class="price">{{ income.value }} </div>
    <div class="date">{{ formattedDate }}</div> 
    <button @click="removeIncome">Remover</button>
  </div>
</template>

<script>
export default {
  props: {
    income: Object
  },
  setup(props, { emit }) {
    const date = new Date(props.income.date);
    const day = date.getDate().toString().padStart(2, '0');
    const month = (date.getMonth()).toString().padStart(2, '0');
    const year = date.getFullYear();
    const formattedDate = `${day}/${month}/${year}`;

    function removeIncome() {
      emit("remove-item", props.income.id);
    }

    return {
      formattedDate,
      removeIncome
    };
  }
};
</script>

<style scoped>
  .income-item {
    position: relative;
    display: flex;
    padding: 15px 15px 15px 0px;
    background-color: #FFF;
    border-radius: 8px;
    max-width: 600px;
    margin: 0 auto 30px;
  }

  .removeItem {
    color: #EF2D2D;
    font-weight: 600;
    font-size: 20px;
    line-height: 1;
    text-align: center;
    margin: 0 15px;
  }

  .desc {
    color: #666;
    flex: 1 1 100%;
    font-size: 20px;
  }

  .price {
    color: #666;
    min-width: 100px;
    font-size: 20px;
  }

  .date {
    color: #666;
    text-align: right;
    font-size: 20px;
  }

  button {
  margin-left: 15px;
  border-radius: 5px;
  padding: 5px;
  background-color: red;
  color: white;
  border: none;
  cursor: pointer;
}
</style>