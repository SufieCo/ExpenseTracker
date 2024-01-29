<template>
  <!-- outerbox  -->
  <div class="w-screen h-screen flex justify-center items-center">
    <!--main frame  -->
    <div class="w-[700px] border border-solid border-black">
      <!-- balance card -->
      <div class="border border-solid divide-y divide-black border-black p-3">
        <div class="p-4">Balance: {{ income + expense }}</div>
        <div class="flex grow border divide-x divide-black">
          <div class="p-4 grow">Income: {{ income }}</div>
          <div class="p-4 grow">Expense: {{ expense }}</div>
        </div>
      </div>
      <!-- inputs -->
      <div class="flex m-3 gap-2">
        <input
          v-model="transactionFormData.description"
          type="text"
          name="description"
          id="item"
          placeholder="decription"
          class="grow rounded-md border-0 py-1 text-gray-900 p-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
        />
        <input
          v-model="transactionFormData.amount"
          type="number"
          name="Amount"
          id="email"
          class="grow rounded-md border-0 py-1.5 text-gray-900 p-2 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
          placeholder="Amount"
        />
        <button
          type="button"
          class="rounded-md bg-indigo-600 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
          @click="addTransaction"
          >
          Add Transaction
        </button>
      </div>
      <Table
        :transactionsList="transactions"
        @deleteTransaction="(index)=>{
          deleteTransaction(index)
        }"
      />
    </div>
  </div>
</template>


<script lang="ts" setup>
  import { computed , ref } from 'vue'
  import Table from './components/table.vue';

  const transactionFormData = ref(
    {
      description:"",
      amount:0
    }
  );

  const transactions = ref([
   {

   }
])

  const income = computed(()=>{
    let sum=0;
    transactions.value.forEach((transaction)=>{
      if(transaction.amount>=0){
        sum = sum + transaction.amount
      }

    })
    return sum
  })

  const expense = computed(()=>{
    let sum=0;
    transactions.value.forEach((transaction)=>{
      if(transaction.amount<0){
        sum = sum + transaction.amount
      }

    })
    return sum
  })

  const addTransaction = () => {
    transactions.value.push({...transactionFormData.value})
  }

  const deleteTransaction = (index:number) =>{
    transactions.value.splice(index,1)
  }
</script>