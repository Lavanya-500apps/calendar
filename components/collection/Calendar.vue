<template>
  <div>
    <div class="flex justify-end absolute left-[33%] top-[1%]">
      <!-- Weekends label starts here -->
      <div>
        <h2>Weekends :</h2>
      </div>
      <!-- To show toggle button to display weekends-->
      <div>
        <Switch
          @click="showWeekEnd()"
          v-model="weekend"
          :class="[
            weekend ? 'bg-indigo-600' : 'bg-gray-200',
            'relative inline-flex h-6 w-11 flex-shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-offset-2',
          ]"
        >
          <span
            aria-hidden="true"
            :class="[
              weekend ? 'translate-x-5' : 'translate-x-0',
              'pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow ring-0 transition duration-200 ease-in-out',
            ]"
          />
        </Switch>
      </div>
    </div>
    <!-- Displaying Calendar view from FullCalendar Component -->
    <div>
      <FullCalendar :options="options" />
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, reactive } from "vue";
import { Switch } from "@headlessui/vue";
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import timeGridPlugin from "@fullcalendar/timegrid";

//forming props
interface calendarOptions {
  plugins: Array<[]>;
  initialView: string;
  weekends: boolean;
  headerToolbar: {
    start: string;
    center: string;
    end: string;
  };
  selectable: boolean;
  events: Array<[]>;
}
const props = withDefaults(defineProps<calendarOptions>(), {
  plugins: [dayGridPlugin, timeGridPlugin],
  initialView: "dayGridMonth",
  weekends: false,
  headerToolbar: {
    start: "prev,next today",
    center: "title",
    end: "dayGridMonth,timeGridWeek,timeGridDay",
  },
  selectable: true,
  events: [{ start: new Date() }],
});

//using props by assiging them to new instance
const { plugins, initialView, headerToolbar, selectable, events } =
  toRefs(props);

let weekend = ref(props.weekends);

const options = computed(() => ({
  plugins: plugins.value,
  initialView: initialView.value,
  weekends: weekend.value,
  headerToolbar: headerToolbar.value,
  selectable: selectable.value,
  events: events.value,
}));

//Click action to show weekends
const showWeekEnd = () => {
  weekend.value = !weekend.value;
};
</script>
