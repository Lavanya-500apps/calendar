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
//importing FullCalendar npm and FullCalendar plugins
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import timeGridPlugin from "@fullcalendar/timegrid";
import interactionPlugin from "@fullcalendar/interaction";

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
  editable: boolean;
  events: Array<[]>;
}
const props = withDefaults(defineProps<calendarOptions>(), {
  plugins: [dayGridPlugin, interactionPlugin, timeGridPlugin], //Plugins To show month,week,day view
  initialView: "dayGridMonth", //set month view as Initial view
  weekends: false, //To display weekends
  headerToolbar: {
    start: "prev,next today",
    center: "title",
    end: "dayGridMonth,timeGridWeek,timeGridDay",
  }, //To display in headers
  editable: true, // important for activating date selectability!
  selectable: true, // important for activating event interactions!
  events: [
    { start: new Date() },
    { title: "event 1", date: "2023-04-01", end: "2023-04-02" },
    { title: "event 2", date: "2023-04-03", end: "2023-04-04" },
  ], //static events
});

//using props by assiging them to new instance
const { plugins, initialView, headerToolbar, selectable, editable, events } =
  toRefs(props);

let weekend = ref(props.weekends);

//eventDetails to Get Events
onMounted(() => {
  eventDetails();
});

const options = computed(() => ({
  plugins: plugins.value,
  initialView: initialView.value,
  weekends: weekend.value,
  headerToolbar: headerToolbar.value,
  selectable: selectable.value,
  editable: editable.value,
  events: events.value,
  select: handleDateSelect,
  eventClick: handleEventClick,
  eventsSet: handleEvents,
}));

//Click action to show weekends
const showWeekEnd = () => {
  weekend.value = !weekend.value;
};

//Get Event data from localstorage
const eventDetails = () => {
  const getEventDetails = localStorage.getItem("eventData");
  if (getEventDetails && getEventDetails.length)
    options.events = JSON.parse(getEventDetails);
};

//Get Selected date information and added events
const handleDateSelect = (selectInfo: any) => {
  let title = ref(prompt("Please enter a new title for your event"));
  let calendarApi = selectInfo.view.calendar;
  calendarApi.unselect(); // clear date selection
  if (title.value) {
    calendarApi.addEvent({
      id: "",
      title: title.value,
      start: selectInfo.startStr,
      end: selectInfo.endStr,
      allDay: selectInfo.allDay,
    });
  }
};

//add new events to events and set events to localstorage
const handleEvents = (event: any) => {
  options.events = event;
  localStorage.setItem("eventData", JSON.stringify(options.events));
  eventDetails();
};

//Delete Event from events
const handleEventClick = (clickInfo: any) => {
  if (
    confirm(
      `Are you sure you want to delete the event '${clickInfo.event.title}'`
    )
  ) {
    clickInfo.event.remove();
    localStorage.setItem("eventData", JSON.stringify(options.events));
    eventDetails();
  }
};
</script>
