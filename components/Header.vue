<template>
    <div flex justify-between items-center>
        <!-- Logo -->
        <LazyCommonLogo />

        <!-- Quick Access -->
        <div flex gap-4>
            <!-- Quick Access Inherted Buttons -->
            <component :is="component" />

            <!-- Home -->

            <ABtn v-if="router.currentRoute.value.name === 'dashboard'" @click="router.push('/tables')" h="70px" text-2xl text-tertiary>
                <IconHome />
            </ABtn>
            <!-- Logout -->
            <ABtn @click="logout()" h="70px" text-2xl text-dangerOp :disabled="loadingLogout">
                <IconLoading v-if="loadingLogout" />
                <IconShutdown v-else />
            </ABtn>
        </div>
    </div>
</template>

<script setup>
const auth = useAuth()
const router = useRouter()
const props = defineProps({
    component: {
        type: Object,
        required: true
    }
})


const loadingLogout = ref(false)

const logout = async () => {
    loadingLogout.value = true
    await new Promise(res => setTimeout(res, 1000));
    loadingLogout.value = false
    auth.signOut()
    router.push('/')
}

</script>