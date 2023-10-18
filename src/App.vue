<template>
  <div class="mainWrapper">
    <header>
      <div class="headerWrapper">
        <h2>Notifications <span v-if="unreadMessages !== 0">{{ unreadMessages }}</span></h2>
        <button role="button" @click="markAllAsRead">Mark all as read</button>
      </div>
    </header>
    <main>
      <div v-for="(item,index) in eventObjects" :key="index">
        <Notification :data="item" :id="index" />
      </div>
    </main>
  </div>
</template>
<script setup>
import { ref } from 'vue'
import { computed } from 'vue';
import Notification from './components/Notifications.vue'
const eventObjects = ref([
  {
    img: '../src/assets/images/avatar-mark-webber.webp',
    isRead: false,
    type: 'reacted',
    userName : 'Mark Webber ',
    events : ' reacted to your recent post',
    targetReaction : 'My first tournament today!',
    time : '1m ago'
  },
  {
    img: '../src/assets/images/avatar-angela-gray.webp',
    isRead: false,
    type: ' followed',
    userName : 'Angela Gray ',
    events : 'followed you',
    time : '5m ago'
  },
  {
    img: '../src/assets/images/avatar-jacob-thompson.webp', 
    isRead: false,
    type: 'group',
    userName : 'Jacob Thompson ',
    events : ' has joined your group',
    targetJoin: 'Chess Club',
    time : '1 day ago'
  },
  {
    img: '../src/assets/images/avatar-rizky-hasanuddin.webp',
    isRead: true,
    type: 'message',
    userName : 'Rizky Hasanuddin ',
    events : ' sent you a private message',
    time : '5 days ago',
    message : "Hello, I wanted to express my gratitude for establishing the Chess Club. I've been a member for a few weeks, and I'm already thoroughly enjoying my time while also seeing improvements in my game."
  },
  {
    img: '../src/assets/images/avatar-kimberly-smith.webp',
    isRead: true,
    type: 'comment',
    userName : 'Kimberly Smith ',
    events : ' commented on your picture',
    targetComment: '../src/assets/images/image-chess.webp',
    time : '1 week ago'
  },
  {
    img: '../src/assets/images/avatar-nathan-peterson.webp',
    isRead: true,
    type: 'reacted',
    userName : 'Nathan Peterson ',
    events : ' reacted to your recent post',
    targetReaction : ' 5 end-game strategies to increase your win rate',
    time : '2 weeks ago'
  },
  {
    img: '../src/assets/images/avatar-anna-kim.webp',
    isRead: true,
    type: 'group',
    targetJoin: 'Chess Club',
    userName : 'Anna Kim ',
    events : ' left the group',
    time : '2 weeks ago'
  },
])
// calculate how many unread messages
function markAllAsRead() {
  eventObjects.value.forEach((item) => {
    item.isRead = true;
  })
  localStorage.setItem('eventObjects', JSON.stringify(eventObjects.value));
}
const unreadMessages = computed(() => {
  return eventObjects.value.filter((item) => !item.isRead).length;
});
const storedData = localStorage.getItem('eventObjects');
if (storedData) {
  eventObjects.value = JSON.parse(storedData);
}
</script>
