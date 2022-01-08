<template>
    <div>
        <div >
            <div class="container-calendar">
                <div class="calendar">
                    <div class="month">
                    <i class="fas fa-angle-left prev" @click="prevCalendarClick"></i>
                    <div class="date">
                        <h1 class="text-xl md:text-5xl text-black">{{this.monthElement}}</h1>
                        <p class="text-black">{{this.yearElement}}</p>
                    </div>
                    <i class="fas fa-angle-right next" @click="nextCalendarClick"></i>
                    </div>
                    <div class="weekdays bg-gray-500">
                      <div>Sun</div>
                      <div>Mon</div>
                      <div>Tue</div>
                      <div>Wed</div>
                      <div>Thu</div>
                      <div>Fri</div>
                      <div>Sat</div>
                    </div>
                    <div class="days">
                      <NuxtLink :to="'/'+monthElement.toLowerCase()+'-'+data.dateValue+'-'+yearElement" v-for="data in daysLists" :key="data.id" :id="data.id" :class="'relative day '+data.dateType" @click.self="dateClick($event)">
                        <div @click.stop.prevent @click="triggerParent($event)" class="h-full w-full flex justify-center items-center">
                          <span class="date-set text-gray-700 font-bold" @click.stop.prevent @click="triggerParentParent($event)">{{data.dateValue}}</span>
                          <span class="sup bg-black" @click.stop.prevent @click="triggerParentParent($event)">1</span>
                        </div>
                      </NuxtLink>
                    </div>
                </div>
                </div>
        </div>
        <ModalEvents v-on:addEventData="addEventDataFunc" v-on:modalToClose="modalDataPass" :selected_date="this.selected_date" :current_time="this.current_time" v-if="calendarModalShow"/>        
    </div>
</template>
<script>
export default {    
    data() {
      return {
          selected_date:{},
          childMessage: [],
          calendarDate: new Date(),          
          current_time: "",  
          monthDays: "",
          lastDay: "",
          lastDate:"", 
          prevLastDay:"",
          firstDayIndex: "",
          lastDayIndex: "",
          lastDayDate: "",
          nextDays: "",
          months: [
              "January",
              "February",
              "March",
              "April",
              "May",
              "June",
              "July",
              "August",
              "September",
              "October",
              "November",
              "December",
          ],
          previousDate:"",
          prevLastDate: "",
          nextDate:"",
          days: "",
          daysLists: [],
          monthElement: "",
          dateElement: "",
          yearElement: "",
          currentEvents: [],
          fullDate: new Date(),
          currentDate: "",
          currentMonth: "",
          currentYear: "",
          selectedDate: "",
          selectedDate: false,
          calendarModalShow: false,
          selectedGlobalElement: "",      
          events:[
            // {
            //   id: 0,
            //   event_title: "Frisy Duty Out na Uli na",
            //   event_description: "Happy Weekend Guys!",
            //   start_date: "November 5, 2021",
            //   end_date: "November 21, 2021",
            //   start_time: "9:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Pantry",
            // },
            // {
            //   id: 1,
            //   event_title: "Frisy Duty Out na Uli na",
            //   event_description: "Happy Weekend Guys!",
            //   start_date: "November 6, 2021",
            //   end_date: "November 21, 2021",
            //   start_time: "9:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Lobby",
            // },
            // {
            //   id: 2,
            //   event_title: "Christmas Party",
            //   event_description: "Yearly Christmas party with the gang!",
            //   start_date: "November 21, 2021",
            //   end_date: "November 21, 2021",
            //   start_time: "5:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 3,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 21, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 4,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 21, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 5,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 21, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 6,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 21, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 7,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 21, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 8,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 21, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 9,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 21, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 10,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 21, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 11,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 22, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 12,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 23, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 13,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 24, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
            // {
            //   id: 14,
            //   event_title: "Release Date for the System",
            //   event_description: "Realese date for the system and presenting it to the public.",
            //   start_date: "November 25, 2021",
            //   end_date: "November 25, 2021",
            //   start_time: "8:00 AM",
            //   end_time: "5:00 PM",
            //   events_location: "Company Warehouse",
            // },
          ],
      }
    },
    methods: {
        addEventDataFunc: function(value){
          var __dictonary = value;
          this.events.push(__dictonary);

          this.selectedDate = this.selectedGlobalElement.target;//Set Selected Date
          let __day = this.selectedDate.querySelector(".date-set").textContent;
          let __month = this.daysLists[this.selectedDate.id].dateMonth;
          let __year = this.daysLists[this.selectedDate.id].dateYear;
          var dictionaryData = {};
          dictionaryData["day"] = __day;
          dictionaryData["month"] = __month;
          dictionaryData["year"] = __year;
          this.selected_date = dictionaryData;

          this.eventsLoad(this.selected_date.day, this.selected_date.month, this.selected_date.year);
        },
        modalDataPass: function(value){
          this.calendarModalShow = value;
        },
        renderCalendar: function(passData) {
            this.daysLists = [];
            const __this = passData;
            this.calendarDate.setDate(1);
            this.monthDays = __this.querySelector(".days");
            this.yearElement = this.calendarDate.getFullYear();

            this.lastDate = new Date(
                this.calendarDate.getFullYear(),
                this.calendarDate.getMonth() + 1,
                0
            );

            this.lastDay = new Date(
                this.calendarDate.getFullYear(),
                this.calendarDate.getMonth() + 1,
                0
            ).getDate();

            this.prevLastDate = new Date(
                this.calendarDate.getFullYear(),
                this.calendarDate.getMonth(),
                0
            );
            this.prevLastDay = new Date(
                this.calendarDate.getFullYear(),
                this.calendarDate.getMonth(),
                0
            ).getDate();
            
            this.firstDayIndex = this.calendarDate.getDay();

            this.lastDayDate = new Date(
                this.calendarDate.getFullYear(),
                this.calendarDate.getMonth() + 1,
                0
            );
            this.lastDayIndex = new Date(
                this.calendarDate.getFullYear(),
                this.calendarDate.getMonth() + 1,
                0
            ).getDay();

            this.nextDays = 14 - this.lastDayIndex - 1;
            this.monthElement = this.months[this.calendarDate.getMonth()];
            this.dateElement = new Date().toDateString();
            for (let x = this.firstDayIndex; x > 0; x--) {
                this.days += `${this.prevLastDay - x + 1}`;
                
                var dictionaryData = {};
                dictionaryData["id"] = this.daysLists.length;
                dictionaryData["dateType"] = "prev-date";
                dictionaryData["dateValue"]= `${this.prevLastDay - x + 1}`;
                dictionaryData["dateMonth"] = this.prevLastDate.getMonth()
                dictionaryData["dateYear"] = this.prevLastDate.getFullYear()
                this.daysLists.push(dictionaryData);
            }
            this.previousDate = this.days;
            for (let i = 1; i <= this.lastDay; i++) {
                if (
                i === new Date().getDate() &&
                this.calendarDate.getMonth() === new Date().getMonth()
                ) {
                    this.days += `<div class="today">${i}</div>`;            
                    var dictionaryData = {};
                    dictionaryData["id"] = this.daysLists.length;
                    if(!this.selectedDate){
                      dictionaryData["dateType"] = "today-date";
                    }else{
                      dictionaryData["dateType"] = "available-date";
                    }
                    dictionaryData["dateValue"]= `${i}`;
                    dictionaryData["dateMonth"] = this.lastDate.getMonth()
                    dictionaryData["dateYear"] = this.lastDate.getFullYear()
                    this.daysLists.push(dictionaryData);    
                } else {
                    this.days += `-${i}-`;
                    var dictionaryData = {};
                    dictionaryData["id"] = this.daysLists.length;
                    dictionaryData["dateType"] = "available-date";
                    dictionaryData["dateValue"]= `${i}`;
                    dictionaryData["dateMonth"] = this.lastDate.getMonth()
                    dictionaryData["dateYear"] = this.lastDate.getFullYear()
                    this.daysLists.push(dictionaryData);    
                }
            }
            for (let j = 1; j <= this.nextDays; j++) {
                this.days += `-${j}-`;
                this.monthDays = this.days;
                var dictionaryData = {};
                dictionaryData["id"] = this.daysLists.length;
                dictionaryData["dateType"] = "next-date";
                dictionaryData["dateValue"]= `${j}`;
                dictionaryData["dateMonth"] = this.lastDayDate.getMonth()
                dictionaryData["dateYear"] = this.lastDayDate.getFullYear()
                this.daysLists.push(dictionaryData);    
            }
        },
        prevCalendarClick: function(){
            const __this = this.$el;
            this.calendarDate.setMonth(this.calendarDate.getMonth() - 1);
            if(__this.querySelectorAll(".today-date").length > 0){
              __this.querySelector(".today-date").classList.remove("today-date")
            }
            this.renderCalendar(__this);
        },
        nextCalendarClick: function(){
            const __this = this.$el;
            this.calendarDate.setMonth(this.calendarDate.getMonth() + 1);
            if(__this.querySelectorAll(".today-date").length > 0){
              __this.querySelector(".today-date").classList.remove("today-date")
            }
            this.renderCalendar(__this);
        },
        dateClick: function(dataEvent){
          const __this = this.$el;
          this.selectedDate = true;
          let selectedElement = dataEvent;
          console.log(selectedElement)
          this.selectedGlobalElement = selectedElement;

          if(selectedElement.target.classList.contains("today-date")){
            const currentDate = this.fullDate.getDate();
            const currentMonth = this.fullDate.getMonth();
            const currentYear = this.fullDate.getFullYear();
            
            this.selectedDate = selectedElement.target;//Set Selected Date
            let __day = this.selectedDate.querySelector(".date-set").textContent;
            let __month = this.daysLists[this.selectedDate.id].dateMonth;
            let __year = this.daysLists[this.selectedDate.id].dateYear;
            var dictionaryData = {};
            dictionaryData["day"] = __day;
            dictionaryData["month"] = __month;
            dictionaryData["year"] = __year;
            if(currentYear <= dictionaryData.year && currentDate <= dictionaryData.day && currentMonth <= dictionaryData.month){
              this.calendarModalShow = true;
              this.selected_date = dictionaryData;
            }
            return false;
          }

          if(__this.querySelectorAll(".today-date").length > 0){
           __this.querySelector(".today-date").classList.remove("today-date");
          }
          selectedElement.target.classList.add("today-date");                
        },
        triggerParent: function(event){
          event.target.parentElement.click()
        },
        triggerParentParent: function(event){
          event.target.parentElement.parentElement.click()
        }
    },
    mounted:function mounted()  {
        const __this = this.$el;
        this.renderCalendar(__this);
        const currentDate = this.fullDate.getDate();
        const currentMonth = this.fullDate.getMonth();
        const currentYear = this.fullDate.getFullYear();
    }
}
</script>

<style scoped>
.container-calendar {
  width: 100%;
  margin: auto;
  height: auto;
  color: #eee;
  display: flex;
  justify-content: center;
  align-items: center;
}

.calendar {
  width: 100%;
  height: auto;
  /* box-shadow: 0 0.5rem 3rem rgba(0, 0, 0, 0.4); */
}

.month {
  width: 100%;
  height: 12rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
  text-align: center;
}

.month i {
  font-size: 2.5rem;
  cursor: pointer;
}

.month h1 {
  font-size: 3rem;
  font-weight: 400;
  text-transform: uppercase;
  letter-spacing: 0.2rem;
  margin-bottom: 1rem;  
}

.month p {
  font-size: 1.6rem;
}

.weekdays {
  width: 100%;
  height: 5rem;
  padding: 0 0.4rem;
  display: flex;
  align-items: center;
  justify-content: center;
}

.weekdays div {
  font-size: 1.5rem;
  font-weight: 400;
  letter-spacing: 0.1rem;  
  display: flex;
  justify-content: center;
  align-items: center;
}

.weekdays > div{
  width: calc(100% / 7);
}

.days {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 0.2rem 0.2rem 15px 0.2rem;
}

.days > a {
  font-size: 1.4rem;
  padding: 0.3rem;
  height: 5rem;
  display: flex;
  justify-content: center;
  align-items: center; 
}
.days > a{
  border: 0.2rem solid transparent;
}

.prev-date,
.next-date {
  opacity: 0.5;
  pointer-events: none;
}
.prev-date .sup,
.next-date .sup{
  background: #8b8b8b;
}
.day.today-date > div {
    background: #000 !important;
}
.day.today-date > div span.date-set{
  color: #fff;
}
i.fas.fa-angle-right.next:before, i.fas.fa-angle-right.next:after {
  content: "";width: 35px;height: 7px;background: #fff;display: block;
}

i.fas.fa-angle-right.next:before {
    transform: rotate(45deg);
    position: relative;
    top: -6px;
}

i.fas.fa-angle-right.next:after {
    transform: rotate(-45deg);
    position: relative;
    top: 8px;
}
i.fas.fa-angle-left.prev:before, i.fas.fa-angle-left.prev:after {
    content: "";
    width: 35px;
    height: 7px;
    background: #fff;
    display: block;
}

i.fas.fa-angle-left.prev:before {
    transform: rotate(45deg);
    position: relative;
    top: 16px;
}

i.fas.fa-angle-left.prev:after {
    transform: rotate(-45deg);
    position: relative;
    top: -12px;
}

.days > a, .weekdays > a {
  width: calc(100% / 7);
}
span.sup {
    position: absolute;
    top: 0;
    right: 0;
    font-size: 13px;
    width: 25px;
    height: 25px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 100px;
    border: solid 1px #fff;
}
span.date-set {
    pointer-events: none;
}
.today-date span.sup{
  pointer-events: none;
}
@media (min-width: 1442px){
  .days > div:hover > div {
    background: gray;
    cursor: pointer;
  }
}
@media (max-width: 1441px){
  .calendar {
    width: 100%
  }
  .container-calendar{
    width: 100%;
  }
  .days > div, .weekdays div{
    width: 100%;
  }
  .days, .weekdays{
    display: grid;
    grid-template-columns: 14% 14% 14% 14% 14% 14% 14% ;
  }
  .weekdays{
    flex-wrap: wrap;
  }
  span.date-set{
    width: 70px;
    text-align: center;
  }
  span.sup{
    top: 5px;
    right: 15px;
  }
}
@media (max-width: 430px){
  .month h1{
    font-size: 20px;
  }
  .month p{
    font-size: 17px;
  }
  .month i{
    transform: scale(0.5);
  }
  .days > div, .weekdays div{
    font-size: 12px;
  }
  span.sup{
    font-size: 8px;
    width: 15px;
    height: 15px;
    top: 12px;
    right: 5px;
    line-height: initial;
  }
  .days > div, .weekdays div{
    height: 35px;
  }
} 
</style>