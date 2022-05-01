<template>
  <div
    class="entry-container mb-3 pointer p-2"
    @click="$router.push({ name: 'entry', params: { id: entry.id }})"
  >
      <!-- Titilo -->
      <div class="entry-title d-flex">
          <span class="text-success fs-5 fw-bold">{{ day }}</span>
          <span class="mx-1 fs-5">{{ month }}</span>
          <span class="mx-2 fw-light">{{ yearDay }}</span>
      </div>

      <div class="entry-description">
          {{ shortText }}
      </div>
  </div>
</template>

<script>
import { computed, ref } from 'vue';

export default {
    props: {
        entry: {
            type: Object,
            required: true,
        }
    },
    setup(props) {
    const months = ref(['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio','Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre']);
    const days   = ref(['Domingo','Lunes','Martes','Miércoles','Jueves','Viernes','Sábado']);

        const funcshortText = computed(() => {
            return ( props.entry.text.length > 130 )
                ? props.entry.text.substring(0,130) + '...'
                : props.entry.text
        }); 
        const day = computed(() => {
            const date = new Date( props.entry.date )
            return date.getDate()
        }); 
        const month = computed(() => {
            const date = new Date( props.entry.date )
            return months.value[ date.getMonth() ]
        });
        const yearDay = computed(() => {
            const date = new Date( props.entry.date )
            return `${ date.getFullYear() }, ${ days.value[ date.getDay() ] }`
        }); 

        return {  
            funcshortText,
            day,
            month,
            yearDay,
        }
    }
}
</script>

<style lang="scss" scoped>
.entry-container {
    border-bottom: 1px solid #2c3e50;
    transition: 0.2s all ease-in;

    &:hover {
        background-color: lighten($color: grey, $amount: 45);
        transition: 0.2s all ease-in;
    }

    .entry-description {
        font-size: 12px;
    }
}

</style>