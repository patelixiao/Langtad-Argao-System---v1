<template>
    <div class="fixed top-0 left-0 h-full w-full bg-black bg-opacity-75 flex justify-center items-start py-10">
        <div class="bg-white w-3/5 relative py-10">
            <h3 class="text-center text-4xl uppercase font-bold">Delete event "Relief Goods Distribution"</h3>
            <div class="flex justify-center items-center mt-10">
                <div class="cursor-pointer bg-black  text-white text-xs px-10 py-4 mx-3" @click="deleteEvent(eventsData)">
                    YES
                </div>
                <div class="cursor-pointer bg-black  text-white text-xs px-10 py-4 mx-3" @click="deleteClick">
                    NO
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['deleteClick', 'eventsData', "deleteEvent"]
}
</script>