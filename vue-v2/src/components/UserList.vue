<template>
    <div>
        <div 
            v-for="(user, index) in userList"
            :key="index"
        >
            <div>{{user.firstName}}</div>
            <div>{{user.lastName}}</div>
        </div>
        <button @click="update">Обновить</button>
    </div>
</template>

<script>
export default {
    name: 'UserList',
    data: () => ({
        userList: []
    }),
    methods: {  
		/** Обновить */
		update() {
            /** Не реактивно, т.к нужно обновить массив целиком, или использовать патченные методы массивов */
            setTimeout(() => {
                this.userList[0] = {firstName: 'Евгений', lastName: 'Вольнов'};
            }, 3000);

            const newUser = {firstName: 'Евгений', lastName: 'Вольнов'};
            setTimeout(() => {
                this.userList = [];
                this.userList.push(newUser);
            }, 6000);

            setTimeout(() => {
                this.userList = [...this.userList, newUser];
            }, 9000);

            setTimeout(() => {
                this.userList.splice(this.userList.length - 1, 1, {firstName: 'Коля', lastName: 'Басков'});
            }, 12000);

            setTimeout(() => {
                newUser.firstName = 'Коля';
                this.userList[this.userList.length - 1].firstName = 'Евгений';
            }, 15000);
		}
    }
}
</script>