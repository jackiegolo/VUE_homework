<script setup>
import DeviceInfo from "@/components/headers/Info.vue";
import DeviceItem from "@/components/devices/Item.vue";
import { ref, reactive } from "vue";
import { v4 as uuidv4 } from "uuid";
const Job = ref("");
const Jobs = reactive([]);

const addJob = () => {
  if (Job !== "") {
    const item = {
      id: uuidv4(),
      title: Job.value,
    };
    Jobs.unshift(item);
    Job.value = "";
  }
};

const removeJob = (id) => {
  const index = Jobs.findIndex((Job) => {
    return Job.id === id
  })
  Jobs.splice(index, 1)
}

</script>

<template>
    <head>
    <meta charset="UTF-8" />
    <link rel="icon" href="/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>TODO APP</title>
    </head>

    <body class="flex flex-col min-h-screen py-8 antialiased bg-slate-50">
    <main class="container mx-auto">
        <header class="m-2">
        <h1 class="text-6xl font-thin select-none">TODO!</h1>
        <div class="font-semibold select-none text-neutral-600">simple and studid todo app</div>
        </header>
        <form class="px-10 py-12 bg-white shadow-sm">
        <section class="flex">
            <input type="text" placeholder="做點重要的事吧..." class="w-full text-2xl focus:outline-none input-lg input input-bordered" v-model="Job" />
            <button @click.prevent="addJob" class="text-xl btn-lg btn btn-neutral">新增</button>
        </section>
        </form>  
        
    <section>
        <header>
            <DeviceInfo :Jobs="Jobs" />
        </header>

        <ul>
            <DeviceItem
                @remove-job-item="removeJob"
                v-for="d in Jobs"
                :Job="d"
            />
        </ul>
    </section>    
    
    </main>
    </body>


    <!-- <form>
        <div class="flex items-center gap-2">
        <input
        type="text"
        placeholder="做點重要的事吧..."
        class="w-full text-2xl focus:outline-none input-lg input input-bordered"
        v-model="Job"
        />       
        <button @click.prevent="addJob" class="text-xl btn-lg btn btn-neutral">新增</button>
        </div>
    </form> -->



</template>

<style scoped></style>
