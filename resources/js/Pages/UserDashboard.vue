<template>
    <div
        class="min-h-screen bg-gradient-to-br from-gray-900 via-teal-950 to-gray-900 text-white"
    >
        <!-- Navigation -->
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
                                User Management
                            </Link>
                            <Link
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

        <!--End of Navigation -->

        <!-- Content -->
        <main class="container mx-auto py-8 px-4">
            <h2 class="text-3xl font-bold mb-8 text-center">User Dashboard</h2>
            <Link
                :href="route('employees.create')"
                :class="[
                    'text-white transition-colors duration-200 mr-4 px-3 py-2 rounded-full',
                    $page.component === 'UserDashboard'
                        ? 'bg-gradient-to-r from-green-400 to-blue-500'
                        : 'hover:bg-gradient-to-r hover:from-green-400 hover:to-blue-500',
                ]"
            >
                CREATE EMPLOYEE
            </Link>

            <!-- Customers Table -->
            <h3 class="text-2xl font-semibold mt-6 mb-4">Customers</h3>
            <div class="overflow-x-auto bg-gray-800 rounded-lg shadow-lg mb-8">
                <table class="w-full">
                    <thead>
                        <tr class="bg-teal-800 text-left">
                            <th class="px-6 py-3 text-sm font-semibold">ID</th>
                            <th class="px-6 py-3 text-sm font-semibold">
                                Name
                            </th>
                            <th class="px-6 py-3 text-sm font-semibold">
                                Email
                            </th>
                            <th class="px-6 py-3 text-sm font-semibold">
                                Actions
                            </th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr
                            v-for="customer in customers"
                            :key="customer.id"
                            class="border-b border-gray-700 hover:bg-gray-700 transition-colors duration-200"
                        >
                            <td class="px-6 py-4">{{ customer.id }}</td>
                            <td class="px-6 py-4">{{ customer.name }}</td>
                            <td class="px-6 py-4">{{ customer.email }}</td>
                            <td class="px-6 py-4">
                                <button
                                    @click="deleteUser(customer.id)"
                                    class="bg-red-600 hover:bg-red-500 text-white px-4 py-2 rounded-lg transition-colors duration-200"
                                >
                                    Delete
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>

            <!-- Employees Table -->
            <h3 class="text-2xl font-semibold mt-6 mb-4">Employees</h3>
            <div class="overflow-x-auto bg-gray-800 rounded-lg shadow-lg">
                <table class="w-full">
                    <thead>
                        <tr class="bg-teal-800 text-left">
                            <th class="px-6 py-3 text-sm font-semibold">ID</th>
                            <th class="px-6 py-3 text-sm font-semibold">
                                Name
                            </th>
                            <th class="px-6 py-3 text-sm font-semibold">
                                Email
                            </th>
                            <th class="px-6 py-3 text-sm font-semibold">
                                Actions
                            </th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr
                            v-for="employee in employees"
                            :key="employee.id"
                            class="border-b border-gray-700 hover:bg-gray-700 transition-colors duration-200"
                        >
                            <td class="px-6 py-4">{{ employee.id }}</td>
                            <td class="px-6 py-4">{{ employee.name }}</td>
                            <td class="px-6 py-4">{{ employee.email }}</td>
                            <td class="px-6 py-4">
                                <button
                                    @click="deleteUser(employee.id)"
                                    class="bg-red-600 hover:bg-red-500 text-white px-4 py-2 rounded-lg transition-colors duration-200"
                                >
                                    Delete
                                </button>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </main>
    </div>
</template>

<script setup>
import { ref } from "vue";
import { Link, router } from "@inertiajs/vue3";
import { ChevronDownIcon, MenuIcon, XIcon } from "lucide-vue-next";
import Dropdown from "@/Components/Dropdown.vue";
import DropdownLink from "@/Components/DropdownLink.vue";

const props = defineProps({
    customers: Array,
    employees: Array,
});

const deleteUser = (id) => {
    if (confirm("Are you sure you want to delete this user?")) {
        router.delete(`/users/${id}`, {
            preserveState: true,
            onSuccess: () => alert("User deleted successfully."),
        });
    }
};
</script>
