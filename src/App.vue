<template>
  <Calendar  @change-date="changeDate" :currentDate="currentDate"></Calendar>
</template>
<script>
import Calendar from './components/Calendar.vue'
export default {
  components:{
    Calendar
  },
  data(){
    return {
        currentDate:new Date()
    }
  },
  methods:{
    changeDate(date){
      this.currentDate = date
    }
  }
}
</script>
<style>

</style>
