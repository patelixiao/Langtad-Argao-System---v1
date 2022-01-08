<template>
    <div  class="pt-20" >
        <div class="w-4/5 m-auto" v-for="data in event" :key="data.id">
            <div class="title-div relative">
                <h1 class="text-center text-4xl uppercase font-bold">{{data.event_name}}</h1>
                <h2 class="text-center">{{data.event_location}}</h2>
                <h2 class="text-center">{{data.event_time}}</h2>
                <div class="absolute top-0 left-0 h-full flex justify-center items-center">
                    <NuxtLink :to="'/'+backLink">Back</NuxtLink>
                </div>
                <div class="absolute top-0 right-0 h-full flex justify-center items-center">
                    <p class="text-7xl no-line-height absolute top-0 right-2 cursor-pointer" @click="optionClick">...</p>
                    <div v-if="optionModal" class="options bg-gray-200 absolute top-24 right-0 w-48 ">
                        <div class="cursor-pointer hover:bg-gray-300 px-4 py-3" @click="editClick(data)">
                            <p>Edit</p>
                        </div>
                        <div class="cursor-pointer hover:bg-gray-300 px-4 py-3" @click="deleteClick(data)">
                            <p>Delete</p>
                        </div>
                    </div>
                </div>
            </div>
            <div class="content-div mt-5">
                <div class="border-b border-gray-400 py-1">
                    <div>
                        <h2 class="text-xl font-bold">Event Details:</h2>
                    </div>
                </div>
                <div id="events-div" class="m-auto block py-1">
                    <div class="" v-html="data.event_content">
                        <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed eget consequat ante. Sed ac est vitae erat consectetur tincidunt at in turpis. Donec euismod eros a lacus ultricies, sit amet bibendum ex molestie. Etiam varius libero non ipsum vehicula, sed facilisis diam varius. Vestibulum vitae magna tempor, porttitor lorem at, facilisis elit. Aenean id erat nec velit iaculis consectetur. Ut sed tortor sed ligula consectetur aliquet. Proin volutpat ultrices erat, a congue lacus euismod a. Nunc nec odio finibus, consequat ligula in, pulvinar mi. Maecenas efficitur vehicula erat eget vehicula. Praesent nec eros quis tellus lobortis pellentesque at et arcu. Vivamus sollicitudin, orci facilisis vulputate porttitor, nunc nulla varius magna, et varius ex tellus quis tortor. Sed in diam augue. Cras eu quam in quam vulputate tristique sit amet eu sem. Quisque maximus, nisi sodales congue interdum, velit nulla vehicula lorem, at volutpat ante felis ut neque.</p>

<p>Suspendisse iaculis mollis fermentum. Morbi malesuada consectetur est, vitae pretium eros pellentesque ac. Proin non sem at sapien ultricies consectetur vitae placerat velit. Ut vitae dui nec neque pellentesque accumsan. Pellentesque eu urna malesuada, convallis nibh nec, maximus erat. Ut dui sem, sagittis a fermentum eget, faucibus vitae urna. Sed porttitor sit amet est sed euismod. Integer volutpat, urna sed volutpat lacinia, augue ante porta libero, quis congue sem nisl nec nunc. Donec ac viverra orci. Aenean arcu quam, convallis sit amet sapien non, tempus dignissim nunc.</p>

<p>Ut at mauris mattis, tristique turpis nec, fermentum felis. Sed gravida pretium ornare. Cras vitae purus vitae metus tincidunt iaculis. Mauris sed nisi metus. Nullam scelerisque sed turpis vitae cursus. Praesent scelerisque pellentesque fermentum. Etiam est dui, pharetra in sapien nec, elementum efficitur libero. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia curae; Proin vehicula dolor id enim tristique placerat. Phasellus auctor tellus et orci scelerisque euismod. Morbi nisi massa, dictum quis erat sit amet, vehicula euismod nisl. Proin accumsan dolor magna, non euismod erat dignissim in.</p>

<p>Donec elementum ornare justo a ullamcorper. Proin sit amet pharetra justo. Nulla elementum vel lorem quis dignissim. Sed lobortis enim vehicula, vehicula eros in, lobortis nulla. Aliquam id scelerisque nibh. Duis ante ex, mollis ut est non, hendrerit elementum magna. Nullam rutrum feugiat varius. In id semper erat, eget faucibus dui. Nullam sed elementum augue. Nulla at orci ut lorem ultricies rhoncus at id mi. Etiam non tincidunt arcu.</p>

<p>Suspendisse mattis iaculis sapien at interdum. Ut ac arcu est. Praesent in urna sit amet tellus consequat tincidunt quis sed neque. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Vestibulum id justo quis enim faucibus imperdiet. Maecenas vitae eleifend orci, iaculis tincidunt ligula. Sed in metus eget lacus pulvinar vestibulum vel eget nisi.</p>

<p>Nulla facilisi. Praesent a lectus nec odio malesuada rhoncus. Praesent auctor convallis felis, elementum lacinia lacus fermentum in. Proin interdum ex vitae imperdiet cursus. Vestibulum vel lobortis orci. Nullam gravida semper lobortis. In facilisis justo et ligula eleifend cursus.</p>

<p>Aenean dignissim felis est, a tincidunt arcu luctus in. Maecenas at felis a sem dapibus hendrerit. Integer tristique vel risus eu scelerisque. Donec consequat molestie elit ut lacinia. Praesent non auctor mauris, eget tincidunt nibh. Cras vestibulum condimentum tortor, quis iaculis tellus vestibulum vitae. Fusce efficitur lectus sapien, vitae imperdiet augue molestie semper. Aliquam molestie nisi et tincidunt ullamcorper.</p>

<p>Duis laoreet nulla eu mauris pharetra, ut mattis enim congue. Sed efficitur, enim a ultricies lobortis, ligula mauris accumsan lectus, sit amet pulvinar purus ipsum sit amet sapien. Morbi scelerisque sollicitudin ex, a aliquam velit porttitor sit amet. In id felis ut enim mattis pretium sit amet sodales orci. Mauris finibus turpis libero, vitae lobortis dui congue sed. Duis ut nulla metus. Phasellus fermentum tincidunt blandit. Quisque quis convallis sem. Donec imperdiet efficitur vulputate. Nunc a est dui. Cras massa ex, iaculis in lorem pellentesque, interdum dignissim purus. Sed convallis tellus eu risus rhoncus, ut interdum felis malesuada. In in ipsum suscipit magna scelerisque cursus.</p>

<p>Pellentesque non iaculis ipsum, vel feugiat odio. Ut tempus quam tellus, non malesuada elit aliquet ut. Duis lacinia nisl eros, nec eleifend ex congue sed. Suspendisse sed nisl eu urna ornare blandit luctus vel justo. Sed ac commodo quam. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Cras quis mi non nisi vulputate pretium. Suspendisse potenti. Curabitur odio diam, dignissim eu varius sed, tincidunt in diam. Mauris a diam est. Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>

<p>Maecenas nibh tellus, finibus ac eleifend a, consectetur eget ante. Donec faucibus magna a sem lacinia bibendum. Aliquam mollis, urna eget rhoncus congue, purus arcu malesuada justo, volutpat dictum mauris dui eget risus. Fusce id mauris dui. Aenean vitae dui mollis, consectetur quam ac, congue mauris. Donec mattis orci sit amet dui dapibus, et maximus elit consectetur. Maecenas at metus a urna interdum faucibus. Nulla commodo sapien mi, non rhoncus mi eleifend at. Integer non justo eget odio rhoncus accumsan. Nunc quis est magna. In hac habitasse platea dictumst. Nullam efficitur fringilla neque venenatis facilisis. Etiam sed luctus lorem. Aliquam erat volutpat. Duis faucibus, felis sit amet luctus venenatis, lorem eros convallis erat, a semper est tortor ut dui. Phasellus mauris sapien, vestibulum ut sapien in, semper tristique metus.</p>
                    </div>
                </div>
            </div>
        </div>
        <!-- Modals Here -->
        <EditEvent v-if="editModal" :editClick="this.editClick" :eventsData="this.editEventsData" v-on:eventDetails="receiveEventEditDetails"/>
        <DeleteEvent v-if="deleteModal" :deleteClick="deleteClick" :eventsData="this.deleteEventsData" :deleteEvent="deleteEvent"/>
    </div>
</template>
<style>
#events-div h1{ 
    font-size: 36px;
}
#events-div h2{ 
font-size: 33px;
}
#events-div h3{ 
font-size: 30px;
}
#events-div h4{ 
font-size: 27px;
}
#events-div h5{ 
font-size: 24px;
}
#events-div h6{ 
font-size: 21px;
}
#events-div p{ 
font-size: 18px;
}
#events-div img{
max-width: 100%;
max-height: auto;
}
#events-div a{ 
font: 18px;
}
</style>
<script>
export default {    
    data() {
      return {
        backLink: "/",
        editModal: false,
        deleteModal: false,
        editEventsData: [],
        deleteEventsData: [],
        event:[],
        events:[
            {
                id: 0,
                event_name: "Event Number 1",
                event_location: "Langtad Basketball Court",
                event_time: "09:00AM - 12:00PM"
            },
            {
                id: 1,
                event_name: "Event Number 2",
                event_location: "Langtad Basketball Court",
                event_time: "09:00AM - 12:00PM"
            },
            {
                id: 2,
                event_name: "Event Number 2",
                event_location: "Langtad Basketball Court",
                event_time: "09:00AM - 12:00PM"
            },
            {
                id: 3,
                event_name: "Event Number 3",
                event_location: "Langtad Basketball Court",
                event_time: "09:00AM - 08:00PM"
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
        optionModal: false,
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
        editClick(value) {
            this.editModal = !this.editModal;
            this.editEventsData = value;
        },
        deleteClick(value) {
            this.deleteModal = !this.deleteModal;
            this.deleteEventsData = value;            
        },
        deleteEvent(value){
            console.log(value)            
            this.events.splice(this.events.indexOf(value), 1);

            this.storeToken("events", JSON.stringify(this.events))

            
            this.deleteModal = !this.deleteModal;
            // let prev_link = JSON.parse(localStorage.getItem("link"));
            // router.push({ name: 'events', params: { prev_link } }) // -> /user/123
            Router.push('/events');
            // window.location.href = "/december-31-2021"
            // router.go(-1)
        },
        receiveEventEditDetails(value) {
            
            value['id'] = this.$route.params._id;
            let event_date = value['event_date'];

            for (let index = 0; index < this.events.length; index++) {
                const element = this.events[index];
                if (element.id == value.id) {
                    this.events[index].event_content = value.event_content;
                    this.events[index].event_location = value.event_location;
                    this.events[index].event_name = value.event_name;
                    this.events[index].event_time = value.event_time;
                }
            }

            this.event = [value];

            this.editModal = !this.editModal;

            this.storeToken("events", JSON.stringify(this.events))
            
            console.log(this.events)
        },
    },
    mounted(){
        this.backLink = localStorage.getItem("link");
        this.events = JSON.parse(localStorage.getItem("events"));

        for(let i = 0; i < this.events.length; i++){
            if(this.events[i].id == this.$route.params._id){
                this.event.push(this.events[i]);
            }
        }
    }
}
</script>