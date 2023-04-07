<template>
    <div class="lg:flex lg:h-full lg:flex-col">
      <header
        class="flex items-center justify-between border-b border-gray-200 px-6 py-4 lg:flex-none"
      >
        <h1 class="text-base font-semibold leading-6 text-gray-900">
          <time datetime="2022-01">January 2022</time>
        </h1>
        <div class="flex items-center">
          <div
            class="relative flex items-center rounded-md bg-white shadow-sm md:items-stretch"
          >
            <div
              class="pointer-events-none absolute inset-0 rounded-md ring-1 ring-inset ring-gray-300"
              aria-hidden="true"
            />
            <button
              type="button"
              class="flex items-center justify-center rounded-l-md py-2 pl-3 pr-4 text-gray-400 hover:text-gray-500 focus:relative md:w-9 md:px-2 md:hover:bg-gray-50"
            >
              <span class="sr-only">Previous month</span>
              <ChevronLeftIcon class="h-5 w-5" aria-hidden="true" />
            </button>
            <button
              type="button"
              class="hidden px-3.5 text-sm font-semibold text-gray-900 hover:bg-gray-50 focus:relative md:block"
            >
              Today
            </button>
            <span class="relative -mx-px h-5 w-px bg-gray-300 md:hidden" />
            <button
              type="button"
              class="flex items-center justify-center rounded-r-md py-2 pl-4 pr-3 text-gray-400 hover:text-gray-500 focus:relative md:w-9 md:px-2 md:hover:bg-gray-50"
            >
              <span class="sr-only">Next month</span>
              <ChevronRightIcon class="h-5 w-5" aria-hidden="true" />
            </button>
          </div>
          <div class="hidden md:ml-4 md:flex md:items-center">
            <Menu as="div" class="relative">
              <MenuButton
                type="button"
                class="flex items-center gap-x-1.5 rounded-md bg-white px-3 py-2 text-sm font-semibold text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 hover:bg-gray-50"
              >
                {{
                  view == "day"
                    ? "Day view"
                    : view == "week"
                    ? "Week view"
                    : view == "year"
                    ? "Year view"
                    : "Month view"
                }}
                <ChevronDownIcon
                  class="-mr-1 h-5 w-5 text-gray-400"
                  aria-hidden="true"
                />
              </MenuButton>
  
  
              <transition
                enter-active-class="transition ease-out duration-100"
                enter-from-class="transform opacity-0 scale-95"
                enter-to-class="transform opacity-100 scale-100"
                leave-active-class="transition ease-in duration-75"
                leave-from-class="transform opacity-100 scale-100"
                leave-to-class="transform opacity-0 scale-95"
              >
                <MenuItems
                  class="absolute right-0 z-10 mt-3 w-36 origin-top-right overflow-hidden rounded-md bg-white shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
                >
                  <div class="py-1">
                    <MenuItem v-slot="{ active }">
                      <button
                        :class="[
                          active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                          'block px-4 py-2 text-sm',
                        ]"
                        @click="openCalender('day')"
                      >
                        Day view
                      </button>
                    </MenuItem>
                    <MenuItem v-slot="{ active }">
                      <button
                        :class="[
                          active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                          'block px-4 py-2 text-sm',
                        ]"
                        @click="openCalender('week')"
                      >
                        Week view
                      </button>
                    </MenuItem>
                    <MenuItem v-slot="{ active }">
                      <button
                        :class="[
                          active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                          'block px-4 py-2 text-sm',
                        ]"
                        @click="openCalender('month')"
                      >
                        Month view
                      </button>
                    </MenuItem>
                    <MenuItem v-slot="{ active }">
                      <button
                        :class="[
                          active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                          'block px-4 py-2 text-sm',
                        ]"
                        @click="openCalender('year')"
                      >
                        Year view
                      </button>
                    </MenuItem>
                  </div>
                </MenuItems>
              </transition>
            </Menu>
            <div class="ml-6 h-6 w-px bg-gray-300" />
            <button
              type="button"
              class="ml-6 rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-500"
            >
              Add event
            </button>
          </div>
          <Menu as="div" class="relative ml-6 md:hidden">
            <MenuButton
              class="-mx-2 flex items-center rounded-full border border-transparent p-2 text-gray-400 hover:text-gray-500"
            >
              <span class="sr-only">Open menu</span>
              <EllipsisHorizontalIcon class="h-5 w-5" aria-hidden="true" />
            </MenuButton>
  
  
            <transition
              enter-active-class="transition ease-out duration-100"
              enter-from-class="transform opacity-0 scale-95"
              enter-to-class="transform opacity-100 scale-100"
              leave-active-class="transition ease-in duration-75"
              leave-from-class="transform opacity-100 scale-100"
              leave-to-class="transform opacity-0 scale-95"
            >
              <MenuItems
                class="absolute right-0 z-10 mt-3 w-36 origin-top-right divide-y divide-gray-100 overflow-hidden rounded-md bg-white shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
              >
                <div class="py-1">
                  <MenuItem v-slot="{ active }">
                    <a
                      href="#"
                      :class="[
                        active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                        'block px-4 py-2 text-sm',
                      ]"
                      >Create event</a
                    >
                  </MenuItem>
                </div>
                <div class="py-1">
                  <MenuItem v-slot="{ active }">
                    <a
                      href="#"
                      :class="[
                        active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                        'block px-4 py-2 text-sm',
                      ]"
                      >Go to today</a
                    >
                  </MenuItem>
                </div>
                <div class="py-1">
                  <MenuItem v-slot="{ active }">
                    <a
                      :class="[
                        active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                        'block px-4 py-2 text-sm',
                      ]"
                    >
                      Day view
                    </a>
                  </MenuItem>
                  <MenuItem v-slot="{ active }">
                    <a
                      :class="[
                        active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                        'block px-4 py-2 text-sm',
                      ]"
                    >
                      Week view
                    </a>
                  </MenuItem>
                  <MenuItem v-slot="{ active }">
                    <a
                      :class="[
                        active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                        'block px-4 py-2 text-sm',
                      ]"
                    >
                      Month view
                    </a>
                  </MenuItem>
                  <MenuItem v-slot="{ active }">
                    <a
                      :class="[
                        active ? 'bg-gray-100 text-gray-900' : 'text-gray-700',
                        'block px-4 py-2 text-sm',
                      ]"
                    >
                      Year view
                    </a>
                  </MenuItem>
                </div>
              </MenuItems>
            </transition>
          </Menu>
        </div>
      </header>
      <collectionDay v-if="view == 'day'"></collectionDay>
      <collectionWeek :weekDays="weekDays" v-if="view == 'week'"></collectionWeek>
      <collectionYear :weekDays="weekDays" v-if="view == 'year'"></collectionYear>
      <div v-else>
        <collectionMonth :weekDays="weekDays" />
      </div>
    </div>
  </template>
  
  
  <script setup lang="ts">
  import {
    ChevronDownIcon,
    ChevronLeftIcon,
    ChevronRightIcon,
    ClockIcon,
    EllipsisHorizontalIcon,
  } from "@heroicons/vue/20/solid";
  import { Menu, MenuButton, MenuItem, MenuItems } from "@headlessui/vue";
  import { ref } from "vue";
  
  
  const props = defineProps({
    // Declare props here
    weekDays: Array,
  });
  const view = ref("");
  const days = [
    { date: "2021-12-27", events: [] },
    { date: "2021-12-28", events: [] },
    { date: "2021-12-29", events: [] },
    { date: "2021-12-30", events: [] },
    { date: "2021-12-31", events: [] },
    { date: "2022-01-01", isCurrentMonth: true, events: [] },
    { date: "2022-01-02", isCurrentMonth: true, events: [] },
    {
      date: "2022-01-03",
      isCurrentMonth: true,
      events: [
        {
          id: 1,
          name: "Design review",
          time: "10AM",
          datetime: "2022-01-03T10:00",
          href: "#",
        },
        {
          id: 2,
          name: "Sales meeting",
          time: "2PM",
          datetime: "2022-01-03T14:00",
          href: "#",
        },
      ],
    },
    { date: "2022-01-04", isCurrentMonth: true, events: [] },
    { date: "2022-01-05", isCurrentMonth: true, events: [] },
    { date: "2022-01-06", isCurrentMonth: true, events: [] },
    {
      date: "2022-01-07",
      isCurrentMonth: true,
      events: [
        {
          id: 3,
          name: "Date night",
          time: "6PM",
          datetime: "2022-01-08T18:00",
          href: "#",
        },
      ],
    },
    { date: "2022-01-08", isCurrentMonth: true, events: [] },
    { date: "2022-01-09", isCurrentMonth: true, events: [] },
    { date: "2022-01-10", isCurrentMonth: true, events: [] },
    { date: "2022-01-11", isCurrentMonth: true, events: [] },
    {
      date: "2022-01-12",
      isCurrentMonth: true,
      isToday: true,
      events: [
        {
          id: 6,
          name: "Sam's birthday party",
          time: "2PM",
          datetime: "2022-01-25T14:00",
          href: "#",
        },
      ],
    },
    { date: "2022-01-13", isCurrentMonth: true, events: [] },
    { date: "2022-01-14", isCurrentMonth: true, events: [] },
    { date: "2022-01-15", isCurrentMonth: true, events: [] },
    { date: "2022-01-16", isCurrentMonth: true, events: [] },
    { date: "2022-01-17", isCurrentMonth: true, events: [] },
    { date: "2022-01-18", isCurrentMonth: true, events: [] },
    { date: "2022-01-19", isCurrentMonth: true, events: [] },
    { date: "2022-01-20", isCurrentMonth: true, events: [] },
    { date: "2022-01-21", isCurrentMonth: true, events: [] },
    {
      date: "2022-01-22",
      isCurrentMonth: true,
      isSelected: true,
      events: [
        {
          id: 4,
          name: "Maple syrup museum",
          time: "3PM",
          datetime: "2022-01-22T15:00",
          href: "#",
        },
        {
          id: 5,
          name: "Hockey game",
          time: "7PM",
          datetime: "2022-01-22T19:00",
          href: "#",
        },
      ],
    },
    { date: "2022-01-23", isCurrentMonth: true, events: [] },
    { date: "2022-01-24", isCurrentMonth: true, events: [] },
    { date: "2022-01-25", isCurrentMonth: true, events: [] },
    { date: "2022-01-26", isCurrentMonth: true, events: [] },
    { date: "2022-01-27", isCurrentMonth: true, events: [] },
    { date: "2022-01-28", isCurrentMonth: true, events: [] },
    { date: "2022-01-29", isCurrentMonth: true, events: [] },
    { date: "2022-01-30", isCurrentMonth: true, events: [] },
    { date: "2022-01-31", isCurrentMonth: true, events: [] },
    { date: "2022-02-01", events: [] },
    { date: "2022-02-02", events: [] },
    {
      date: "2022-02-03",
      events: [
        {
          id: 7,
          name: "Cinema with friends",
          time: "9PM",
          datetime: "2022-02-04T21:00",
          href: "#",
        },
      ],
    },
    { date: "2022-02-04", events: [] },
    { date: "2022-02-05", events: [] },
    { date: "2022-02-06", events: [] },
  ];
  const selectedDay = days.find((day) => day.isSelected);
  const openCalender = (value: any) => {
    view.value = value;
  };
  </script>