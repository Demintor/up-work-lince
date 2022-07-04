<template>
	<div>
		<div class="user__info">
			<div class="user__info-first-name">
				{{user.firstName}}
			</div>
			<div class="user__info-last-name">
				{{user.lastName}}
			</div>
		</div>
		<button @click="update">Обновить</button>
	</div>
</template>

<script>

export default {
	name: "User",
	data: () => ({
		user: {}
	}),
	methods: {
		/** Обновить реактивно */
		update() {
            setTimeout(() => {
                this.user.firstName = 'Евгений'; // Не реактивно, т.к Observer не знает о свойствах объекта user
			    this.user = Object.assign(this.user, { lastName: 'Вольнов' }); // Не реактивно, необходимо создать новый объект
            }, 3000);

            setTimeout(() => {
                this.user = {};
                this.$set(this.user, 'firstName', 'Евгений');
            }, 6000);
            setTimeout(() => {
                this.user = Object.assign({}, this.user, {firstName: 'Евгений', lastName: 'Вольнов'});
            }, 9000);

            const newUser = {firstName: 'Евг', lastName: 'Вол'};
			setTimeout(() => {
			    this.user = {...newUser};
            }, 12000);
            setTimeout(() => {
                this.user = newUser;
                newUser.firstName = 'Коля';
                newUser.lastName = 'Басков';
            }, 15000);
		}
	}
};
</script>

<style>
	.user__info {
		margin-bottom: 10px;
	}
</style>