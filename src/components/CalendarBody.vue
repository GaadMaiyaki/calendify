<template>
  <div class="container">

    <div class="mt-4 text-center text-muted text-dark p-2">
      <span class="text-muted bg-light text-dark p-2 rounded shadow-sm">Calender App using Vue js</span>
    </div>
    
    <div class="mt-5 d-flex align-items-center">
      <div class="text-info px-2 py-1 shadow-sm" style="flex: 6">
        <h6 class="text-capitalize font-weight-light">
          <span class="text-info bg-light p-1">Pick a date here</span>
        </h6>
      </div>
      <div style="flex: 6">
        <select class="custom-select custom-select-sm shadow-sm" @change="handleChange($event)">
          <option v-for="year in pushYears" :key="year">{{ year }}</option>
        </select>
      </div>
    </div>
    
    <div v-if="checkEmpty" class="mt-5">
      <h3 class="p-3 text-muted text-center font-weight-light"> No match found.</h3>
    </div>
    <div class="row mb-5" v-if="changedShow && checkEmpty === false">
      <div class="col-sm-12 col-md-6 col-lg-6 col-xl-6" v-for="i of 12" :key="i" >
        <div class="text-center">
          <div class=" px-2 mt-5">
            <div class="text-left text-muted">
              <strong>{{ displayDay(i) }}</strong>
            </div>
          </div>
          <div class="mt-1 d-flex p-2 border border-info border-top-0 border-bottom-0 rounded flex-wrap shadow-sm">
            <div v-for="(day, i) of days" :key="day" class="py-2" style="width: 14%">
              <span :class = "(i & 1) !== 0 ? styles[0] : styles[1] ">{{ day }}</span>
            </div>
          </div>
        </div>

        <div class="text-center">
          <div class=" d-flex p-2 border border-info border-top-0 rounded flex-wrap shadow justify-content-start">
            <div v-for="num in startDate(currentYear, (+currentMonth - 1) + i)" :key="num" class="py-2" style="width: 14%">
              <span class= ""></span>
            </div>
            <div v-for="num in daysInAMonth(currentYear, currentMonth + i)" :key="num" class="py-2" style="width: 14%">
              <span :class= "circleDate(num, i)">{{ num }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>

  </div>  
  
</template>

<script>
export default {
    
    name: 'Calender',

    mounted(){
      this.loopingYear();
    },


    data(){
      return{
        
        styles:
          [
            'bg-light px-2 py-2 text-muted rounded mx-1 shadow-sm', 
            'bg-white px-2 py-2 text-muted rounded mx-1 shadow-sm',
            'p-2 text-light bg-success font-weight-bold rounded rounded-circle'
          ],
        
        days: ['Sun', 'Mon', 'Tue', 'Wed', 'Thur', 'Fri', 'Sat'],
        months: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'Novemver', 'December'],
        currentMonth: new Date().getMonth(),
        currentYear: new Date().getFullYear(),
        currentYearA: new Date().getFullYear(),
        loopYearStart: 1970,
        loopYearStop: 2051,
        pushYears: [''],
        changedShow: true,
        pickedYear: new Date().getFullYear(),
        pickedMonth: '',
        checkEmpty: false
      }
    },

    methods:{
      circleDate(num, i){
        const cirlce = new Date(this.currentYear, this.currentMonth, num).toDateString();
        const now = new Date().toDateString();
        return cirlce === now && i === this.currentMonth + 1 ? this.styles[2] : '';
      },
      daysInAMonth(year, month){
        return new Date(+year, +month - 1, 0).getDate();
      },

      startDate(year, month){
        return new Date(+year, (month - 1), 1).getDay();
      },

      displayDay(index){
        return `${ this.months[index - 1] } ${ this.currentYear }`;
      },

      loopingYear(){
        
        for(let i = this.loopYearStart; i < this.loopYearStop; i++){
          this.pushYears.push(i);
        }
      },

      handleChange(e){
        if(e.target.value === ""){
          this.currentYear = new Date().getFullYear();
          this.changedShow = false;
          this.checkEmpty = true;
        }
        else{
          this.currentYear = e.target.value;
          this.pickedYear = e.target.value;
          this.checkEmpty = false;
          this.changedShow = true;
        }
      
      }
    },

    computed:{
      day:{
        get() {
            return new Date().getDay() + 7;
        },
      },
      month:{
        get() {
            return new Date().toLocaleString('default', { month: 'long' });
        },
      },
      year:{
        get(){
          return new Date().getFullYear();
        }
      }
    }
    
}
</script>

<style scoped>
  
</style>