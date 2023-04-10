<template>
  <div>
    <div class="flex justify-start">
      <div>
        <h2>Weekends :</h2>
      </div>
      <div>
        <Switch
          @click="showWeekEnd()"
          v-model="enabled"
          :class="[
            enabled ? 'bg-indigo-600' : 'bg-gray-200',
            'relative inline-flex h-6 w-11 flex-shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-indigo-600 focus:ring-offset-2',
          ]"
        >
          <span
            aria-hidden="true"
            :class="[
              enabled ? 'translate-x-5' : 'translate-x-0',
              'pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow ring-0 transition duration-200 ease-in-out',
            ]"
          />
        </Switch>
      </div>
    </div>
    <div>
      <FullCalendar :options="calendarOptions" />
    </div>
  </div>
</template>
<script setup lang="ts">
import { ref, reactive } from "vue";
import { Switch } from "@headlessui/vue";
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import timeGridPlugin from "@fullcalendar/timegrid";

const enabled = ref(false);

const calendarOptions = reactive({
  plugins: [dayGridPlugin, timeGridPlugin],
  initialView: "dayGridMonth",
  weekends: enabled.value,
  headerToolbar: {
    start: "prev,next today",
    center: "title",
    end: "dayGridMonth,timeGridWeek,timeGridDay",
  },
  events: [{ start: new Date() }],
});
const showWeekEnd = () => {
  (enabled.value = !enabled.value), (calendarOptions.weekends = enabled.value);
};
</script>
