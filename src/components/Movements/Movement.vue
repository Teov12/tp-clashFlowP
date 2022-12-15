<script setup>
import { defineProps, toRefs, computed, defineEmits } from "vue";
const props = defineProps({
    id: Number,
    title: String,
    description: String,
    amount: Number
})

const {id ,title, description, amount} = toRefs(props)


const emit = defineEmits(["remove"])

const remove = () => {
    emit("remove", id.value)
}

const isNegative = computed(()=>amount.value < 0)


const movementAmount = computed(()=>{
  return currencyFormatter.format(amount.value)
})

const currencyFormatter = new Intl.NumberFormat("es-AR", {
 style: "currency",
 currency: "ARS",
});




</script>

<template>  
    <div class="movement">
        <div class="content">
            <h4>{{title}}</h4>
            <p>{{description}}</p>
        </div>
        <div class="action">
            <img src="./trash-icon.svg" alt="borrar" @click="remove"/>
            <p :class="{ 'red': isNegative, 'green': !isNegative }">{{movementAmount}}</p>
        </div>
    </div>
</template>


<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 100%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
    color: red;
}
.green {
    color: green;
}
</style>