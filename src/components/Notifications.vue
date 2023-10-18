<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <div class="eventWrapper" :class=" {isUnread : !props.data.isRead}">
        <img class="imageNotifications" :src="img" :alt="userName" />
        <div class="innerNotifications">
            <div class="notificationContent">
                <p v-html="stringGenerator(type)"></p>
                <div v-if="!props.data.isRead" class="unreadPing"></div>
            </div>
            <p class="time">{{ time }}</p>
            <div class="messageWrapper" v-if="type === 'message'">
                <p>{{ message }}</p>
            </div>
    </div>
  <img class="imageNotifications" v-if="type === 'comment'" :src="targetComment" />
</div>

</template>
<script setup>
import { defineProps } from 'vue'
const props = defineProps({
    data: Object,
    id: Number
})
const { img, type, userName, events, time, message,targetComment,targetReaction, targetJoin } = props.data;
// differentiate the string template for the notification based on the type of notification
function stringGenerator(type) {
    switch (type) {
        case 'reacted':
            return `<span class='profileName'>${userName}</span> ${events} <strong class="targetReaction">${targetReaction}</strong>`
        case 'followed':
            return `<span class='profileName'>${userName}</span> ${events}`
        case 'group':
            return `<span class='profileName'>${userName}</span> ${events} <strong class='targetJoin'>${targetJoin}</strong>`
        case 'message':
            return `<span class='profileName'>${userName}</span> ${events}`
        case 'comment':
            return `<span class='profileName'>${userName}</span> ${events}`
        default:
            return `<span class='profileName'>${userName}</span> ${events}`
    }
}
</script>
<style lang="scss">
@import './Notifications.scss'; // Import your SCSS file
</style>