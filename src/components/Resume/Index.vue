<script setup>
import { computed, defineProps, toRefs } from "vue"

const props = defineProps({
    labeltotal: {
        type: String,
        default: null
    },
    label: String,
    monto: {
        type: Number,
        default: null
    },
    montototal:Number,
})

const {label, monto, montototal, labeltotal} = toRefs(props);

const montoVisual = computed(()=>{
    return monto.value !== null ? monto.value : montototal.value
});
const labelVisual = computed(()=>{
    return label.value !== null ? label.value : labeltotal.value
})
const montoCurrency = computed(()=>{
    return currencyFormatter.format(montoVisual.value);
})

const currencyFormatter = new Intl.NumberFormat("es-AR", {
 style: "currency",
 currency: "ARS",
});


</script>

<template>
    <main>
        <p>{{ labelVisual }}</p>
        <h1>{{ montoCurrency }}</h1>
        <div class="graphic">
            <slot name="graphic"></slot>
        </div>
        <div class="action">
            <slot name="action"></slot>
        </div>
    </main>
</template>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}
h1,
p {
  margin: 0;
  text-align: center;
}
h1 {
  margin-top: 14px;
  color: var(--brand-green);
}
.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>


