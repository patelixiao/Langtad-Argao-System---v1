<template>
    <div class="pt-20">
        <div class="title-div relative w-4/5 m-auto border-b border-gray-300">
            <div class="m-2 relative">
                <h1 class="text-center text-4xl uppercase font-bold">{{months[new Date(this.$route.params._id).getMonth()]}} {{new Date(this.$route.params._id).getDate()}} , {{new Date(this.$route.params._id).getFullYear()}}</h1>
                <NuxtLink to="/" class="absolute top-0 left-0 h-full flex justify-center items-center">Back</NuxtLink>
                <div class="absolute top-0 right-0 h-full flex justify-center items-center">
                    <p class="text-7xl no-line-height absolute top-0 right-2 cursor-pointer" @click="optionClick">...</p>
                    <div v-if="optionModal" class="options bg-gray-200 absolute top-12 right-0 w-48 ">
                        <div class="cursor-pointer hover:bg-gray-300 px-4 py-3" @click="addClick">
                            <p>Add</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="content-div mt-5">
            <div v-if="filteredEventsLength > 0" class="w-4/5 m-auto grid grid-cols- sm:grid-cols-3">
                <NuxtLink :to="'/events/'+event.id" v-for="event in filteredEvents" :key="event.id" class="event-item p-2">
                    <div class="border border-gray-400 p-2">
                        <div class="title-div">
                            <h2 class="text-2xl font-bold">{{event.event_name}}</h2>
                        </div>
                        <div class="details-div">
                            <h3><span>{{event.event_location}}</span> | <span>{{event.event_time}}</span></h3>
                        </div>
                    </div>
                </NuxtLink>
            </div>
            <div v-else class="w-4/5 m-auto">
                <h2 class="text-2xl font-bold text-center mt-10">No events available.</h2>
            </div>
        </div>
        <!-- Modals here -->
        <AddEvent v-if="addEventModal" :addClick="this.addClick" :saveClick="this.saveClick" v-on:eventDetails="receiveEventDetails"/>
        <!-- <tinymce id="d1" :other_options="tinyOptions" v-model="editorContent"></tinymce> -->
    </div>
</template>
<style scoped>
.no-line-height{  
    line-height: 0;
}  
</style>
<script>
import Vue from 'vue';
import tinymce from 'vue-tinymce-editor';
Vue.component('tinymce', tinymce);

export default {    
    data() {
      return {
        addEventModal: false,
        optionModal: false,
        filteredEvents: [],
        filteredEventsLength: 0,
        tinyOptions: {
            'height': 250,
            'convert_urls': true,
            'link_assume_external_targets':true,
            'default_link_target': '_blank',
            plugins: [
                'advlist autolink lists link image charmap print preview anchor',
                'searchreplace visualblocks code fullscreen',
                'insertdatetime media table paste code help wordcount '
            ],  
        },
        events:[
            {
                id: 0,
                event_name: "Relief Goods Distribution",
                event_location: "Langtad Argao Cebu",
                event_time: "09:00AM - 12:00PM",
                event_date: "december-31-2021",
                event_content: "TESTING 1"
            },
            {
                id: 1,
                event_name: "Event Number 2",
                event_location: "Langtad Basketball Court",
                event_time: "09:00AM - 12:00PM",
                event_date: "december-10-2021",
                event_content: "TESTING 1"
            },
            {
                id: 2,
                event_name: "Event Number 2",
                event_location: "Langtad Basketball Court",
                event_time: "09:00AM - 12:00PM",
                event_date: "december-20-2021",
                event_content: "TESTING 1"
                
            },
            {
                id: 3,
                event_name: "Event Number 3",
                event_location: "Langtad Basketball Court",
                event_time: "09:00AM - 08:00PM",
                event_date: "december-20-2021",
                event_content: "TESTING 1"
            },
        ],
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
      }
    },
    methods:{
        storeToken(tokenname,token) {
            if(process.client) {
                localStorage.setItem(tokenname, token)
            }
        },
        optionClick() {
            this.optionModal = !this.optionModal;
        },
        addClick() {
            this.addEventModal = !this.addEventModal;
        },
        receiveEventDetails(value) {
            value['id'] = this.events.length;
            value['event_date'] = this.$route.params._id;
            this.events.push(value);
            this.filteredEvents.push(value);
            this.filteredEventsLength = this.filteredEvents.length;
            this.addClick();

            this.storeToken("events", JSON.stringify(this.events))
            console.log(this.filteredEvents)
        },
        
    },
    computed: {
        // filteredEvents() {
        //     let filteredEvents = [];
        //     for(let i = 0; i < this.events.length ; i++)
        //         if(this.events[i].event_date == this.$route.params._id)
        //             filteredEvents.push(this.events[i])
        //     this.filteredEventsLength = filteredEvents.length;
        //     return filteredEvents;
        // }
    },
    mounted(){
        this.storeToken("link", this.$route.params._id)
        if(localStorage.getItem("events") == undefined || localStorage.getItem("events") == null)
            this.storeToken("events", JSON.stringify(this.events))

        this.events = JSON.parse(localStorage.getItem("events"));

        let filteredEvents = [];
            for(let i = 0; i < this.events.length ; i++){
                if(this.events[i].event_date == this.$route.params._id){
                    filteredEvents.push(this.events[i])
                }
            }
            this.filteredEvents = filteredEvents;
            this.filteredEventsLength = filteredEvents.length;
    }
}
</script>