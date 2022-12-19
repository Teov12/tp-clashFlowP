<script setup>
import Header from "./Header.vue";
import Layout from "./Layout.vue";
import Resume from "./Resume/Index.vue"
import Movements from "./Movements/Index.vue"
import Action from "./Action.vue"
import Graphic from "./Resume/Graphic.vue"
import { ref } from "@vue/reactivity";
import { computed, onMounted } from "@vue/runtime-core";

const monto = ref(null);
const label = ref(null);
const movements = ref([]);

onMounted(()=>{
  const movementss = JSON.parse(localStorage.getItem("movements"));
  console.log(movementss);

  if (Array.isArray(movementss)) {
    movements.value = movementss?.map(m =>{
    return {...m, time: new Date(m.time)};
  });
  }
})

//agregar movimiento
const create = (movement) =>{
  const nextId = Math.max(...movements.value.map((movement) => movement.id)) + 1;
  movements.value.push({
    id:nextId,
    ...movement,
  })
  save();
}

//eliminar movimiento
const remove = (id) => {
movements.value = movements.value.filter(m => m.id != id);
save()
}

//guardar movimientos en la memoria
const save = () =>{
  localStorage.setItem("movements", JSON.stringify(movements.value))
}

const select = (el) =>{
  console.log(el);
  monto.value = el;
};

const totalAmount = computed(()=>{
  return movements.value.reduce((suma, m)=>{
    return suma + m.amount
  }, 0);
})


const amounts = computed(()=>{
  const lastDays = movements.value
        .filter(m => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
          return m.time > oldDate;
        })
        .map(m => m.amount);
      
      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);
        return lastMovements.reduce((suma, movement) => {
          return suma + movement
        }, 0);
  })
})
</script>

<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>

    <template #resume>
      <Resume 
          :label="'Ahorro total'" 
          :labeltotal="label"
          :monto= "monto" 
          :montototal= "totalAmount">
        
        <template #graphic>
          <Graphic
            :amounts="amounts"
            @select="select"
          />
        </template>

        <template #action>
          <Action 
          @create="create"/>
        </template>
      </Resume>
    </template>

    <template #movements>
      <Movements 
        :movements="movements"
        @remove="remove">
      </Movements>
    </template>

  </Layout>
</template>

<style>

</style>