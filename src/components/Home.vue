<script setup>
import Header from "./Header.vue";
import Layout from "./Layout.vue";
import Resume from "./Resume/Index.vue"
import Movements from "./Movements/Index.vue"
import { ref } from "@vue/reactivity";

const monto = ref(null)
const label = ref(null)
const movements = ref([{
          id: 0,
          title: "Movimiento",
          description: "Deposito de salario",
          amount: 1000,
        },
        {
          id: 1,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: 500,
        },
        {
          id: 2,
          title: "Movimiento 3",
          description: "Comida",
          amount: -100,
        },
        {
          id: 3,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: 1000,
        },
        {
          id: 4,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: 1000,
        },
]);
</script>

<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>

    <template #resume>
      <Resume 
        :labeltotal="label"
        label="Ahorro total" 
        :monto= "monto" 
        montototal= 10000002 >

        <template #graphic>
          graphiccc
        </template>

        <template #action>
          actionnn
        </template>
      </Resume>
    </template>

    <template #movements>
      <Movements :movements="movements"></Movements>
    </template>

  </Layout>
</template>

<style>

</style>