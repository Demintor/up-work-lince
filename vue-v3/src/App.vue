<template>
	<div id="app">
		<User class="user"/>
		<UserList />
	</div>
</template>

<script>
import User from './components/User.vue';
import UserList from './components/UserList.vue'
export default {
	name: "App",
	components: {User, UserList}
};
</script>

<style scoped>
	.user {
		margin-bottom: 15px;
	}
</style>
