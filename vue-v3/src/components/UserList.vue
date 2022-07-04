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
		/** Обновить*/
		update() {
            /** стало реактивно, Proxy перехватывает любые обращения к this.userList */
            setTimeout(() => {
                this.userList[0] = {firstName: 'Евгений', lastName: 'Вольнов'}; // Стало реактивно
            }, 3000);
            
            const newUser = {firstName: 'Коля', lastName: 'Басков'};
            setTimeout(() => {
                this.userList.push(newUser);
            }, 6000);

            /** 
             * Изменение поля по ссылке теперь не реактивно, 
             * так как this.userList обернут в прокси,
             * и Proxy не перехватывает изменение элемента по ссылке
             */
            setTimeout(() => {
                newUser.firstName = 'Евгений';
                console.log(newUser, this.userList[this.userList.length - 1], newUser === this.userList[this.userList.length - 1]);
            }, 9000);
		}
    }
}
</script>