<script setup>
import BreezeAuthenticatedLayout from "@/Layouts/Authenticated.vue";
import { Head, Link, useForm } from "@inertiajs/inertia-vue3";
defineProps({
  posts: Array
});
const form = useForm();
function destroy(id) {
  if (confirm("Are you sure you want to Delete")) {
    form.delete(route("posts.destroy", id));
  }
}
</script>
<template>
  <Head title="Dashboard" />
  <BreezeAuthenticatedLayout>
    <template #header>
      <h2
        class="font-semibold text-xl text-gray-800 leading-tight"
      >Laravel 9 Vue JS CRUD App using Vite Example - LaravelTuts.com</h2>
    </template>
    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div class="bg-white overflow-hidden shadow-sm sm:rounded-lg">
          <div class="p-6 bg-white border-b border-gray-200">
            <div class="flex items-center justify-between mb-6">
              <Link
                class="px-6 py-2 text-white bg-green-500 rounded-md focus:outline-none"
                :href="route('posts.create')"
              >Create Post</Link>
            </div>
            <table class="table-fixed w-full">
              <thead>
                <tr class="bg-gray-100">
                  <th class="px-4 py-2 w-20">No.</th>
                  <th class="px-4 py-2">Title</th>
                  <th class="px-4 py-2">Body</th>
                  <th class="px-4 py-2">Action</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="post in posts">
                  <td class="border px-4 py-2">{{ post.id }}</td>
                  <td class="border px-4 py-2">{{ post.title }}</td>
                  <td class="border px-4 py-2">{{ post.body }}</td>
                  <td class="border px-4 py-2">
                    <Link
                      tabindex="1"
                      class="px-4 py-2 text-sm text-white bg-blue-500 rounded"
                      :href="route('posts.edit', post.id)"
                    >Edit</Link>
                    <button
                      @click="destroy(post.id)"
                      tabindex="-1"
                      type="button"
                      class="mx-1 px-4 py-2 text-sm text-white bg-red-500 rounded"
                    >Delete</button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </BreezeAuthenticatedLayout>
</template>