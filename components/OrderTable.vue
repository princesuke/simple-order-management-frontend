<template>
  <div class="mt-6">
    <table class="w-full border-collapse border border-gray-300">
      <thead>
        <tr class="bg-gray-200">
          <th class="border p-2">ID</th>
          <th class="border p-2">Product</th>
          <th class="border p-2">Quantity</th>
          <th class="border p-2">Order Date</th>
          <th class="border p-2">Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="order in orders" :key="order.id" class="text-center">
          <td class="border p-2">{{ order.id }}</td>
          <td class="border p-2">{{ order.productName }}</td>
          <td class="border p-2">{{ order.quantity }}</td>
          <td class="border p-2">
            {{ new Date(order.orderDate).toLocaleDateString() }}
          </td>
          <td class="border p-2">
            <span
              :class="
                order.status === 'Pending'
                  ? 'text-yellow-500'
                  : 'text-green-500'
              "
            >
              {{ order.status }}
            </span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const orders = ref([]);

const fetchOrders = async () => {
  try {
    const res = await fetch("https://localhost:7027/api/Orders");
    orders.value = await res.json();
  } catch (error) {
    console.error("Error fetching orders:", error);
  }
};

onMounted(fetchOrders);
</script>
