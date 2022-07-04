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
		/** Обновить */
		update() {
            /** стало реактивно, Proxy перехватывает любые обращения к this.user */
            setTimeout(() => {
                this.user.firstName = 'Евгений';
			    this.user = Object.assign(this.user, { lastName: 'Вольнов' });
            }, 3000);
		}
	}
};
</script>

<style>
	.user__info {
		margin-bottom: 10px;
	}
</style>