<template>
    <div class="fixed top-0 left-0 h-full w-full bg-black bg-opacity-75 flex justify-center items-start py-10">
        <div class="bg-white w-11/12">
            <div class="title border-b border-gray-200">
                <h1 class="text-3xl uppercase font-bold px-5 py-2">
                    <span class="float-right cursor-pointer" @click="this.editClick">×</span>Edit Event
                </h1>
            </div>
            <div class="px-5 py-2">
                <div class="flex">
                    <div class="my-1 w-1/3 mr-1">
                        <input type="text" v-model="event_name" class="event-name border border-gray-500 px-4 py-2 w-full rounded" name="event-name" id="event-name" placeholder="Event Title">
                    </div>
                    <div class="my-1 w-1/3 ml-1 mr-1">
                        <input type="text" v-model="event_location" class="event-place border border-gray-500 px-4 py-2 w-full rounded" name="event-place" id="event-place" placeholder="Event Place">
                    </div>
                    <div class="my-1 w-1/3 ml-1">
                        <input type="time" v-model="event_time" class="event-time border border-gray-500 px-4 py-2 w-full rounded" name="event-time" id="event-time" placeholder="Event Time">
                    </div>
                </div>
                <div>
                    <tinymce id="d1" :other_options="tinyOptions" v-model="event_content" ></tinymce>
                </div>
                <div>
                    <p @click="addData" class="px-4 py-2 bg-black text-white cursor-pointer w-auto mt-2 text-center rounded">Save</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Vue from 'vue';
import tinymce from 'vue-tinymce-editor';
Vue.component('tinymce', tinymce);

export default {    
    props: ['editClick','eventsData', 'saveClick'],
    data() {
        return {
            optionModal: false,
            event_name: '',
            event_location: '',
            event_time: '',
            event_content: '<h2 style="color: #339966;">Hi there from TinyMCE for Vue.js.</h2> <p>&nbsp;</p> <p><span>Hey y`all.</span></p>',
            tinyOptions: {
                'height': 350,
                'convert_urls': true,
                'link_assume_external_targets':true,
                'default_link_target': '_blank',
                plugins: [
                    'advlist autolink lists link image charmap print preview anchor',
                    'searchreplace visualblocks code fullscreen',
                    'insertdatetime media table paste code help wordcount '
                ],  
            },
        }
    },
    methods:{ 
        addData(){ 
            var dic = {};
            dic['event_name'] = this.event_name;
            dic['event_location'] = this.event_location;
            dic['event_time'] = this.event_time;
            dic['event_content'] = this.event_content;
            // console.log(dic)
            this.$emit('eventDetails', dic)
        }
    },
    mounted(){
        this.event_name = this.eventsData.event_name;
        this.event_location = this.eventsData.event_location;
        this.event_time = this.eventsData.event_time;
        this.event_content = this.eventsData.event_content;

        tinyMCE.execCommand('mceRemoveControl',true,'d1');
        tinyMCE.execCommand('mceAddControl',true,'d1');                  
        
        tinyMCE.activeEditor.setContent(this.event_content); 
        
    }
}
</script>