<template>
    <div>
        <div stlye="background:red;">
            <div class="container">
                <div class="calendar">
                    <div class="month">
                    <i class="fas fa-angle-left prev" @click="prevCalendarClick">&#10094;</i>
                    <div class="date">
                        <h1>{{this.monthElement}}</h1>
                    </div>
                    <i class="fas fa-angle-right next" @click="nextCalendarClick">&#10095;</i>
                    </div>
                    <div class="weekdays">
                    <div>Sun</div>
                    <div>Mon</div>
                    <div>Tue</div>
                    <div>Wed</div>
                    <div>Thu</div>
                    <div>Fri</div>
                    <div>Sat</div>
                    </div>
                    <div class="days">
                        
                    </div>
                </div>
                </div>
        </div>
    </div>
</template>
<script>
export default {
    data() {
        return {
            calendarDate: new Date(),            
            monthDays: "",
            lastDay: "",
            prevLastDay:"",
            firstDayIndex: "",
            lastDayIndex: "",
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
            nextDate:"",
            days: "",
            daysLists: [],
            monthElement: "",
            dateElement: "",
        }
    },
    methods: {
        renderCalendar: function(passData) {
            this.daysLists = [];
            const __this = passData;
            
            this.calendarDate.setDate(1);
            this.monthDays = __this.querySelector(".days");

              this.lastDay = new Date(
                this.calendarDate.getFullYear(),
                this.calendarDate.getMonth() + 1,
                0
            ).getDate();

            this.prevLastDay = new Date(
                this.calendarDate.getFullYear(),
                this.calendarDate.getMonth(),
                0
            ).getDate();
            
            this.firstDayIndex = this.calendarDate.getDay();

            this.lastDayIndex = new Date(
                this.calendarDate.getFullYear(),
                this.calendarDate.getMonth() + 1,
                0
            ).getDay();

            this.nextDays = 7 - this.lastDayIndex - 1;

            this.monthElement = this.months[this.calendarDate.getMonth()];
            this.dateElement = new Date().toDateString();

            for (let x = this.firstDayIndex; x > 0; x--) {
                this.days += `${this.prevLastDay - x + 1}`;
                var dictionaryData = {};
                dictionaryData["dateType"] = "previous-date";
                dictionaryData["dateValue"]= `${this.prevLastDay - x + 1}`;
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
                    dictionaryData["dateType"] = "today-date";
                    dictionaryData["dateValue"]= `${i}`;
                    this.daysLists.push(dictionaryData);    
                } else {
                    this.days += `-${i}-`;
                    var dictionaryData = {};
                    dictionaryData["dateType"] = "available-date";
                    dictionaryData["dateValue"]= `${i}`;
                    this.daysLists.push(dictionaryData);    
                }
            }
            for (let j = 1; j <= this.nextDays; j++) {
                this.days += `-${j}-`;
                this.monthDays = this.days;
                var dictionaryData = {};
                dictionaryData["dateType"] = "next-date";
                dictionaryData["dateValue"]= `${j}`;
                this.daysLists.push(dictionaryData);    
            }
            console.log(this.daysLists)
            var HTMLset ="";
            for(let i = 0; i < this.daysLists.length; i++){
              HTMLset += "<div class='days "+this.daysLists[i].dateType+"'>"+this.daysLists[i].dateValue+"</div>"
            }
            __this.querySelector(".days").innerHTML = HTMLset;
        },
        prevCalendarClick: function(){
            const __this = this.$el;
            this.calendarDate.setMonth(this.calendarDate.getMonth() - 1);
            this.renderCalendar(__this);
        },
        nextCalendarClick: function(){
            const __this = this.$el;
            this.calendarDate.setMonth(this.calendarDate.getMonth() + 1);
            this.renderCalendar(__this);
        },
    },
    mounted:function mounted()  {
        const __this = this.$el;
        this.renderCalendar(__this);
    }
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Quicksand", sans-serif;
}

html {
  font-size: 62.5%;
}

.container {
  width: 100%;
  height: 100vh;
  background-color: #12121f;
  color: #eee;
  display: flex;
  justify-content: center;
  align-items: center;
}

.calendar {
  width: 45rem;
  height: 52rem;
  background-color: #222227;
  box-shadow: 0 0.5rem 3rem rgba(0, 0, 0, 0.4);
}

.month {
  width: 100%;
  height: 12rem;
  background-color: #991b1b;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2rem;
  text-align: center;
  text-shadow: 0 0.3rem 0.5rem rgba(0, 0, 0, 0.5);
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
}

.weekdays div {
  font-size: 1.5rem;
  font-weight: 400;
  letter-spacing: 0.1rem;
  width: calc(44.2rem / 7);
  display: flex;
  justify-content: center;
  align-items: center;
  text-shadow: 0 0.3rem 0.5rem rgba(0, 0, 0, 0.5);
}

.days {
  width: 100%;
  display: flex;
  flex-wrap: wrap;
  padding: 0.2rem;
}

.days div {
  font-size: 1.4rem;
  width: calc(44.2rem / 7);
  padding: 0.3rem;
  height: 5rem;
  display: flex;
  justify-content: center;
  align-items: center;
  text-shadow: 0 0.3rem 0.5rem rgba(0, 0, 0, 0.5);
  transition: background-color 0.2s;
}

.days div:hover:not(.today) {
  background-color: #262626;
  border: 0.2rem solid #777;
  cursor: pointer;
}

.prev-date,
.next-date {
  opacity: 0.5;
}

.today {
  background-color: #167e56;
}
.days {
    background: #222227;
}
.days.today-date {
    background: #991b1b;
}
</style>