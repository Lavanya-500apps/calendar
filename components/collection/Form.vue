<template>
  <div>
    <!-- Add Event button  -->
    <div class="flex justify-end absolute left-[10%] top-0.5%]">
      <button
        @click="open = true"
        type="button"
        class="rounded-md bg-indigo-600 px-3.5 py-2.5 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
      >
        Add Event
      </button>
    </div>
    <!-- Start for sidebar -->
    <TransitionRoot as="template" :show="open">
      <Dialog as="div" class="relative z-10" @close="open = false">
        <div class="fixed inset-0" />

        <div class="fixed inset-0 overflow-hidden">
          <div class="absolute inset-0 overflow-hidden">
            <div
              class="pointer-events-none fixed inset-y-0 right-0 flex max-w-full pl-10 sm:pl-16"
            >
              <TransitionChild
                as="template"
                enter="transform transition ease-in-out duration-500 sm:duration-700"
                enter-from="translate-x-full"
                enter-to="translate-x-0"
                leave="transform transition ease-in-out duration-500 sm:duration-700"
                leave-from="translate-x-0"
                leave-to="translate-x-full"
              >
                <DialogPanel class="pointer-events-auto w-screen max-w-md">
                  <form
                    @submit.prevent="saveEvent"
                    class="flex h-full flex-col divide-y divide-gray-200 bg-white shadow-xl"
                  >
                    <div class="h-0 flex-1 overflow-y-auto">
                      <div class="bg-indigo-700 px-4 py-6 sm:px-6">
                        <div class="flex items-center justify-between">
                          <DialogTitle
                            class="text-base font-semibold leading-6 text-white"
                            >Add Event</DialogTitle
                          >
                          <div class="ml-3 flex h-7 items-center">
                            <button
                              type="button"
                              class="rounded-md bg-indigo-700 text-indigo-200 hover:text-white focus:outline-none focus:ring-2 focus:ring-white"
                              @click="open = false"
                            >
                              <span class="sr-only">Close panel</span>
                              <XMarkIcon class="h-6 w-6" aria-hidden="true" />
                            </button>
                          </div>
                        </div>
                      </div>
                      <div class="flex flex-1 flex-col justify-between">
                        <div class="divide-y divide-gray-200 px-4 sm:px-6">
                          <div
                            class="relative mt-6 flex-1 px-4 sm:px-6 border ml-2 mr-2"
                          >
                            <div class="mt-2">
                              <label
                                for="name"
                                class="block text-sm font-medium leading-6 text-gray-900"
                              >
                                Event</label
                              >
                              <div class="mt-2">
                                <input
                                  required
                                  type="text"
                                  id="title"
                                  v-model="form.title"
                                  class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                                  placeholder="Enter Event Name"
                                />
                              </div>
                            </div>
                            <div class="mt-2">
                              <label
                                for="name"
                                class="block text-sm font-medium leading-6 text-gray-900"
                              >
                                Date</label
                              >
                              <input
                                required
                                type="date"
                                id="date"
                                v-model="form.date"
                                class="pl-2 block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:text-sm sm:leading-6"
                              />
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                    <div class="flex flex-shrink-0 justify-end px-4 py-4">
                      <button
                        type="button"
                        class="rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
                        @click="open = false"
                      >
                        Cancel
                      </button>
                      <button
                        type="submit"
                        class="ml-4 inline-flex justify-center rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600"
                      >
                        Save
                      </button>
                    </div>
                  </form>
                </DialogPanel>
              </TransitionChild>
            </div>
          </div>
        </div>
      </Dialog>
    </TransitionRoot>
    <!-- End of sidebar -->
    <!-- import calendar component to show calendar view -->
    <collectionCalendar v-if="show" :events="events" />
  </div>
</template>

<script setup lang="ts">
import {
  Dialog,
  DialogPanel,
  DialogTitle,
  TransitionChild,
  TransitionRoot,
} from "@headlessui/vue";
import { XMarkIcon } from "@heroicons/vue/24/outline";
import { ref } from "vue";

const open = ref(false);
const show = ref(false);
let events = ref([]);
const form = ref({
  title: "",
  date: "",
});
//eventDetails to Get Events
onMounted(() => {
  eventDetails();
  show.value = true;
});

//Get Event data from localstorage
const eventDetails = () => {
  const getEventDetails = localStorage.getItem("eventData");
  if (getEventDetails && getEventDetails.length)
    events.value = JSON.parse(getEventDetails);
};
//add new events to events and set events to localstorage
const saveEvent = () => {
  events.value.push(form.value);
  localStorage.setItem("eventData", JSON.stringify(events.value));
  open.value = false;
  form.value = {};
};
</script>
