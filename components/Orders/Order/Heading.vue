<template>
    <div flex justify-between items-center>
        <div flex gap-4 text-tertiary>
            <div flex flex-col>
                <span text-sm font-bold>Total</span>
                <span text-warningOp p-3 rounded-lg font-bold text-xl bg-secondaryOp w-200px>
                    {{ usePrice(total) }}
                </span>
            </div>
            <div flex flex-col>
                <span text-sm font-bold>Opened By</span>
                <span text-white p-3 rounded-lg font-bold text-xl bg-secondaryOp w-200px>
                    {{ openedBy }}
                </span>
            </div>
            <div flex flex-col>
                <span text-sm font-bold>Table</span>
                <span text-white p-3 rounded-lg font-bold text-xl bg-secondaryOp w-200px>
                    {{ order?.table_number ?? 'Delivery' }}
                </span>
            </div>
            <div flex flex-col>
                <span text-sm font-bold>Order</span>
                <span text-white p-3 rounded-lg font-bold text-xl bg-secondaryOp w-200px>
                    {{ order?.id ?? '#' }}
                </span>
            </div>
        </div>

        <!-- Title -->
        <span font-bold text-3xl text-white>{{ categoriesStore.getSelected?.name ?? 'Categories' }}</span>
    </div>
</template>

<script setup>
const categoriesStore = useCategories()
const ordersStore = useOrders()
const order = ordersStore.getOrder
// watch(() => ordersStore.order?.order_products, () => {
//     total.value = order?.order_products?.reduce((acc, item) => acc + item.price * item.quantity, 0) ?? 0
// }, { deep: true, immediate: true })
const total = computed(() => order?.order_products?.reduce((acc, item) => acc + item.price * item.quantity, 0) ?? 0)

const openedBy = computed(() => order?.order_users.find((user) => user.status === 1)?.name ?? 'Unknown')
</script>