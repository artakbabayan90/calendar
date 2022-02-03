<template>
  <div>
    <div class="calendar-wrapper">
      <h1>
        <div><span class="change-year"
                   @click="changeDate(currentDate.getFullYear()-1,currentDate.getMonth(),currentDate.getDate())">&lt;</span>{{
            currentDate.getFullYear()
          }}<span
              class="change-year"
              @click="changeDate(currentDate.getFullYear()+1,currentDate.getMonth(),currentDate.getDate())">&gt;</span>
        </div>
        <select name="month"
                @change="changeDate(currentDate.getFullYear(),monthNames.indexOf($event.target.value),currentDate.getDate())">
          <option v-for="month in monthNames" :key="month"
                  :selected="month === monthNames[currentDate.getMonth()]">
            {{ month }}
          </option>
        </select>
      </h1>
      <ol class="calendar">
        <li class="day-name" v-for="day in weekDays">{{ day }}</li>
        <li :style="weekDay" :class="{'active':currentDate.getDate() === 1}"
            @click="changeDate(currentDate.getFullYear(),currentDate.getMonth(),1)">1
        </li>
        <li v-for="index in monthDays-1" :key="index+'day'" :class="{'active':currentDate.getDate() === index+1}"
            @click="changeDate(currentDate.getFullYear(),currentDate.getMonth(),index+1)">{{ index + 1 }}
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calendar",
  data() {
    return {
      monthNames: ["January", "February", "March", "April", "May", "June",
        "July", "August", "September", "October", "November", "December"
      ],
      weekDays:['Sun','Mon','Tue','Wed','Thu','Fri','Sat'],
      // currentDate: new Date(),
    }
  },
  props:{
    currentDate:{
      type:Date,
      required:true
    }
  },
  computed: {
    monthDays() {
      return new Date(this.currentDate.getFullYear(), this.currentDate.getMonth() + 1, 0).getDate();
    },
    weekDay() {
      return {'grid-column-start': new Date(this.currentDate.getFullYear(), this.currentDate.getMonth(), 1).getDay() + 1};
    }
  },
  methods: {
    changeDate(year, month, day) {
      this.$emit('change-date',new Date(year, month, day))
    }
  }

}
</script>

<style scoped>
.calendar-wrapper {
  max-width: 280px;
  font: 100% system-ui;
}

.calendar {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
}


.day-name {
  background: #eee;
}

h1 {
  text-align: center;
}

.active {
  color: white;
  background-color: #2c3e50;
}

ol {
  list-style: none;
  margin: 0;
  padding: 0;
  text-align: center;
}

li {
  cursor: pointer;
  padding: 2px;
}

.change-year {
  cursor: pointer;
}
</style>