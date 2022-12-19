<script setup>
import Header from "./Header.vue";
import Layout from "./Layout.vue";
import Resume from "./Resume/Index.vue"
import Movements from "./Movements/Index.vue"
import Action from "./Action.vue"
import Graphic from "./Resume/Graphic.vue"
import { ref } from "@vue/reactivity";
import { computed } from "@vue/runtime-core";

const monto = ref(null)
const label = ref(null)
const movements = ref([
        {
          id: 0,
          title: "Movimiento 1",
          description: "Deposito de salario",
          amount: 100,
          time: new Date("12-11-2022"),
        },
        {
          id: 1,
          title: "Movimiento 2",
          description: "Deposito de honorarios",
          amount: 200,
          time: new Date("12-12-2022"),
        },
        {
          id: 2,
          title: "Movimiento 3",
          description: "Comida",
          amount: 500,
          time: new Date("12-13-2022"),
        },
        {
          id: 3,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: 200,
          time: new Date("12-14-2022"),
        },
        {
          id: 4,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: -400,
          time: new Date("12-14-2022"),
        },
        {
          id: 5,
          title: "Movimiento 6",
          description: "Reparación equipo",
          amount: -600,
          time: new Date("12-15-2022"),
        },
        {
          id: 6,
          title: "Movimiento 7",
          description: "Reparación equipo",
          amount: -300,
          time: new Date("12-11-2022"),
        },
        {
          id: 7,
          title: "Movimiento 8",
          description: "Reparación equipo",
          amount: 0,
          time: new Date("9-12-2022"),
        },
        {
          id: 8,
          title: "Movimiento 9",
          description: "Reparación equipo",
          amount: 300,
          time: new Date("12-2-2022"),
        },
        {
          id: 9,
          title: "Movimiento 10",
          description: "Reparación equipo",
          amount: 500,
          time: new Date("12-12-2022"),
        },     
]);

const amounts = computed(()=>{
  const lastDays = movements.value
        .filter(m => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
          return m.time > oldDate;
        })
        .map(m => m.amount);
      
      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i);
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
          label="Ahorro total" 
          :labeltotal="label"
          :monto= "monto" 
          montototal= 10000002>
        
        <template #graphic>
          <Graphic
            :amounts="amounts"
          />
        </template>

        <template #action>
          <Action/>
        </template>
      </Resume>
    </template>

    <template #movements>
      <Movements 
        :movements="movements">
      </Movements>
    </template>

  </Layout>
</template>

<style>

</style>