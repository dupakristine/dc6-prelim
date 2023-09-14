<script setup>
import Layout from '@/Layouts/Layout.vue';
import { Head } from '@inertiajs/vue3';
</script>


<template>
    <Head title="Clients" />

    <Layout>
        <div class="flex flex-wrap justify-center">
            <div v-for="client in clients.data" :key="client.id" class="m-4">
                <!-- Client Card -->
                <div class="bg-blue-900 text-white p-4 rounded-lg w-72">
                    <div class="grid place-content-center">
                        <img width="170" src="pic.png" alt="">
                    </div>
                    <div class="text-center mt-3">
                        <div class="text-lg font-semibold">{{ client.first_name }} {{ client.last_name }}</div>
                        <div class="text-gray-400">{{ client.address }}</div>
                        <div class="text-gray-400">{{ client.phone }}</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Add Space Here -->
        <div style="margin-top: 20px;"></div>

        <div style="display: grid; place-items: center;">
            <div class="mt-4 flex flex-col items-center space-y-4">
                <div class="flex items-center space-x-2">
                    <span v-if="clients.prev_page_url">
                        <a
                            :href="clients.prev_page_url"
                            @click.prevent="$inertia.visit(clients.prev_page_url)"
                            class="pagination-link text-sm font-medium text-gray-100 bg-gray-900 hover:bg-gray-700 px-3 py-2 rounded-md transition duration-100"
                        >
                            Previous
                        </a>
                    </span>

                  <!-- Numbered Links Pagination -->
    <template v-if="clients.last_page > 1">
        <nav aria-label="Pagination">
            <ul class="flex space-x-2">
                 <!-- Page Links (Limited to 5 Pages) -->
                <template v-for="page in Math.min(5, clients.last_page)" :key="page">
                     <li>
                         <a
                              :href="'/clients?page=' + page"
                              @click.prevent="$inertia.visit('/clients?page=' + page)"
                              class="pagination-link text-sm font-medium text-gray-100 bg-gray-800 hover:bg-gray-700 px-3 py-2 rounded-md transition duration-100"
                              :class="{ 'bg-gray-600': page === clients.current_page }" >
                             {{ page }}
                        </a>
                     </li>
                </template>
            </ul>
        </nav>
    </template>

    <span v-if="clients.current_page < clients.last_page && clients.current_page !== 5">
    <a
        :href="clients.next_page_url"
        @click.prevent="$inertia.visit(clients.next_page_url)"
        class="pagination-link text-sm font-medium text-gray-100 bg-gray-900 hover:bg-gray-700 px-3 py-2 rounded-md transition duration-100"
    >
        Next
    </a>
    </span>

                </div>
            </div>
        </div>
    </Layout>
</template>

<script>
export default {
    props: {
        clients: Object, // Define the clients prop type as an object
    },
};
</script>
