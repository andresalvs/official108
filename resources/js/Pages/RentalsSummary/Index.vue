<template>
    <div
        class="min-h-screen bg-gradient-to-br from-gray-900 via-teal-950 to-gray-900 text-white"
    >
        <header class="bg-gray-900 shadow-lg">
            <div class="container mx-auto px-4 py-4">
                <div class="flex justify-between items-center">
                    <div class="text-2xl font-bold tracking-tighter">
                        <span
                            class="inline-block text-transparent bg-clip-text bg-gradient-to-r from-teal-300 to-blue-500 group-hover:from-blue-500 group-hover:to-purple-400 transition-all duration-300 transform hover:scale-105 hover:shadow-lg"
                        >
                            ZoomPro
                        </span>
                    </div>

                    <!-- Desktop -->

                    <div class="flex items-center space-x-4">
                        <nav class="hidden md:block">
                            <Link
                                :href="route('UserDashboard')"
                                :class="[
                                    'text-white transition-colors duration-200 mr-4 px-3 py-2 rounded-full',
                                    $page.component === 'UserDashboard'
                                        ? 'bg-gradient-to-r from-green-400 to-blue-500'
                                        : 'hover:bg-gradient-to-r hover:from-green-400 hover:to-blue-500',
                                ]"
                            >
                                User Management </Link
                            ><Link
                                :href="route('CameraDashboard')"
                                :class="[
                                    'text-white transition-colors duration-200 mr-4 px-3 py-2 rounded-full',
                                    $page.component === 'CameraDashboard'
                                        ? 'bg-gradient-to-r from-green-400 to-blue-500'
                                        : 'hover:bg-gradient-to-r hover:from-green-400 hover:to-blue-500',
                                ]"
                            >
                                Camera Management
                            </Link>

                            <Link
                                :href="route('rentals-summary.index')"
                                :class="[
                                    'text-white transition-colors duration-200 mr-4 px-3 py-2 rounded-full',
                                    $page.component === 'RentalsSummary'
                                        ? 'bg-gradient-to-r from-green-400 to-blue-500'
                                        : 'hover:bg-gradient-to-r hover:from-green-400 hover:to-blue-500',
                                ]"
                            >
                                Summary
                            </Link>
                            <Link
                                :href="route('activity-logs.index')"
                                :class="[
                                    'text-white transition-colors duration-200 mr-4 px-3 py-2 rounded-full',
                                    $page.component === 'ActivityLogs'
                                        ? 'bg-gradient-to-r from-green-400 to-blue-500'
                                        : 'hover:bg-gradient-to-r hover:from-green-400 hover:to-blue-500',
                                ]"
                            >
                                Activity Logs
                            </Link>
                        </nav>
                        <!-- Settings Dropdown -->
                        <Dropdown align="right" width="48">
                            <template #trigger>
                                <button
                                    class="flex items-center text-white hover:text-teal-400 transition-colors duration-200"
                                >
                                    <span>{{
                                        $page.props.auth.user.name
                                    }}</span>
                                    <ChevronDownIcon class="ml-2 h-4 w-4" />
                                </button>
                            </template>

                            <template #content>
                                <DropdownLink :href="route('profile.edit')"
                                    >Profile</DropdownLink
                                >
                                <DropdownLink
                                    :href="route('logout')"
                                    method="post"
                                    as="button"
                                    >Log Out</DropdownLink
                                >
                            </template>
                        </Dropdown>

                        <!-- Mobile Menu Button -->
                        <button
                            @click="
                                showingNavigationDropdown =
                                    !showingNavigationDropdown
                            "
                            class="md:hidden text-white focus:outline-none"
                        >
                            <MenuIcon
                                v-if="!showingNavigationDropdown"
                                class="h-6 w-6"
                            />
                            <XIcon v-else class="h-6 w-6" />
                        </button>
                    </div>
                </div>

                <!-- Mobile Navigation -->
                <div v-show="showingNavigationDropdown" class="md:hidden mt-4">
                    <nav class="space-y-2">
                        <Link
                            :href="route('UserDashboard')"
                            :class="[
                                'block py-2 px-3 rounded-full text-white transition-colors duration-200',
                                $page.component === 'UserDashboard'
                                    ? 'bg-gradient-to-r from-green-400 to-blue-500'
                                    : 'hover:bg-gradient-to-r hover:from-green-400 hover:to-blue-500',
                            ]"
                        >
                            User Management
                        </Link>
                        <Link
                            :href="route('CameraDashboard')"
                            :class="[
                                'block py-2 px-3 rounded-full text-white transition-colors duration-200',
                                $page.component === 'CameraDashboard'
                                    ? 'bg-gradient-to-r from-green-400 to-blue-500'
                                    : 'hover:bg-gradient-to-r hover:from-green-400 hover:to-blue-500',
                            ]"
                        >
                            Camera Management
                        </Link>
                        <Link
                            :href="route('rentals-summary.index')"
                            :class="[
                                'block py-2 px-3 rounded-full text-white transition-colors duration-200',
                                $page.component === 'RentalsSummary'
                                    ? 'bg-gradient-to-r from-green-400 to-blue-500'
                                    : 'hover:bg-gradient-to-r hover:from-green-400 hover:to-blue-500',
                            ]"
                        >
                            Summary
                        </Link>
                        <Link
                            :href="route('activity-logs.index')"
                            :class="[
                                'block py-2 px-3 rounded-full text-white transition-colors duration-200',
                                $page.component === 'ActivityLogs'
                                    ? 'bg-gradient-to-r from-green-400 to-blue-500'
                                    : 'hover:bg-gradient-to-r hover:from-green-400 hover:to-blue-500',
                            ]"
                        >
                            Activity Logs
                        </Link>
                    </nav>
                </div>
            </div>
        </header>

        <main class="container mx-auto py-8 px-4">
            <h1>Rentals Summary</h1>
            <!-- Refresh Button -->
            <button
                @click="refreshData"
                class="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
            >
                Refresh Data
            </button>

            <table class="mt-4 w-full border-collapse border">
                <thead>
                    <tr>
                        <th class="border p-2">Category</th>
                        <th class="border p-2">Total Rentals</th>
                        <th class="border p-2">Total Revenue</th>
                    </tr>
                </thead>
                <tbody>
                    <tr
                        v-for="summary in rentalsSummary"
                        :key="summary.camera_category"
                    >
                        <td class="border p-2">
                            {{ summary.camera_category }}
                        </td>
                        <td class="border p-2">
                            {{ summary.total_rentals }}
                        </td>
                        <td class="border p-2">
                            {{ formatCurrency(summary.total_revenue) }}
                        </td>
                    </tr>
                </tbody>
            </table>
            <div class="mb-4 p-4 bg-gray-800 rounded-lg text-white">
                <h2 class="text-lg font-semibold">Total Revenue</h2>
                <p class="text-3xl font-bold">
                    {{ formatCurrency(totalRevenue) }}
                </p>
            </div>
        </main>
    </div>
</template>

<script setup>
import Dropdown from "@/Components/Dropdown.vue";
import DropdownLink from "@/Components/DropdownLink.vue";

import { router, Link } from "@inertiajs/vue3";
import { ChevronDownIcon, MenuIcon, XIcon } from "lucide-vue-next";

// Props received from the server-side
const props = defineProps({
    rentalsSummary: Array,
    totalRevenue: Number,
});

// Refresh function to fetch updated data
const refreshData = () => {
    router.reload({
        only: ["rentalsSummary", "totalRevenue"], // Specify the props to reload
        preserveScroll: true, // Optional: preserve the user's scroll position
        onSuccess: () => {
            console.log("Data refreshed successfully");
        },
        onError: (errors) => {
            console.error("Error refreshing data:", errors);
        },
    });
};

// Currency formatting function
const formatCurrency = (value) => {
    return new Intl.NumberFormat("en-US", {
        style: "currency",
        currency: "USD",
    }).format(value);
};
</script>
