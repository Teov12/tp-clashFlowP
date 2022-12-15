<script setup>
import Modal from "./Modal.vue"
import {ref} from "vue"
const showModal = ref(false)
const title = ref("");
const monto = ref(0);
const descipcion= ref("");
const movementType = ref("Ingreso")

const close = function(){
    showModal.value = false
}

const submit = () => {
    showModal.value = !showModal.value
}

</script>

<template>
    <button @click="showModal = true">Agregar Movimiento</button>
    <teleport to="#app">
        <Modal v-show="showModal" @close="close">
            <form @submit.prevent="submit">

                <div class="field">
                    <label for="Titulo">Titulo</label>
                    <input type="text" v-model="title"/>
                </div>

                <div class="field">
                    <label for="Monto">Monto</label>
                    <input type="text" v-model="monto">
                </div>

                <div class="field">
                    <label for="Descripcion">Descripcion</label>
                    <textarea cols="4" v-model="descipcion"></textarea>
                </div>

                <div class="field">
                    <label class="radio-label">
                        <input type="radio" v-model="movementType" value="Ingreso">
                        <span>Ingreso</span>
                    </label>
                    
                    <label class="radio-label">
                        <input type="radio" v-model="movementType" value="Gasto">
                        <span>Gasto</span>
                    </label>
                </div>

                <div class="action">
                    <button type="submit">Agregar movimiento</button>
                </div>

            </form>
        </Modal>
    </teleport>
</template>

<style scoped>
button {
  color: white;
  font-size: 1.25rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
  box-sizing: border-box;
}

form {
  font-size: 1.24rem;
  width: 100%;
}

form .action {
  padding: 0 24px;
}

.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}

input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}

input[type="number"] {
  text-align: right;
}

.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}

.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}

input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--brand-blue);
  border: 2px solid var(--brand-blue);
  border-radius: 50%;
}

input[type="radio"]:checked {
  background-color: var(--brand-blue);
}
</style>