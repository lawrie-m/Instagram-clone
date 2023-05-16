<script setup>
import { RouterLink, useRouter } from "vue-router"
import Container from "./Container.vue"
import AuthModal from "./AuthModal.vue"
import {useUserStore} from "../stores/users"
import { ref } from "vue"
import { storeToRefs } from "pinia"

const userStore = useUserStore()

const {user, loadingUser} = storeToRefs(userStore)
const router = useRouter()
const searchUsername = ref("")

const onSearch = () => {
    if (searchUsername.value) {
        router.push(`/profile/${searchUsername.value}`)
        searchUsername.value = ""
    }
}

const handleLogout = async () => {
    await userStore.handleLogout()
}

const goToUsersProfile = () => {
    router.push(`/profile/${user.value.username}`)
}

</script>

<template>
    <a-layout-header>
        <Container>
            <div class="nav-container flex justify-between">
                <div class="right-content !flex !items-center">
                    <router-link class="mr-2.5" to="/">Instagram</router-link>
                    <a-input-search
                        v-model:value="searchUsername"
                        placeholder="username..."
                        style="width: 200px"
                        @search="onSearch"
                    />
                </div>
                <div class="content flex items-center" v-if="!loadingUser">
                    <div class="flex items-center" v-if="!user">
                        <AuthModal :is-login="true"/>
                        <AuthModal :is-login="false"/>
                    </div>
                    <div class="flex items-center" v-else>
                        <a-button class="ml-2.5" type="primary" @click="goToUsersProfile">Profile</a-button>
                        <a-button class="ml-2.5" type="primary" @click="handleLogout">Logout</a-button>
                    </div>
                </div>
            </div>
        </Container>
    </a-layout-header>
</template>

<style scoped>
/* .nav-container {
    display: flex;
    justify-content: space-between;
} */

/* .content {
    display: flex;
    align-items: center;
} */

/* .right-content{
    display: flex;
    align-items: center;
} */

/* .right-content a {
    margin-right: 10px;
} */

.left-content {
    display: flex;
    align-items: center;
}

/* .left-content button {
    margin-left: 10px;
} */

</style>