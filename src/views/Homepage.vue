<template>
  <v-container>
    <h1 class="mb-5">Explore Product V1</h1>

    <form>
      <v-text-field
        v-model="form.product_name_id"
        label="Product Name Indonesia"
      ></v-text-field>

      <v-text-field
        v-model="form.product_name_en"
        label="Product Name English"
      ></v-text-field>

      <v-select
        v-model="form.destination"
        :items="destination"
        item-title="name"
        item-value="id"
        label="Select Destination"
      ></v-select>

      <v-textarea v-model="form.description" label="Description"></v-textarea>

      <v-text-field
        v-model="form.qty"
        label="Total QTY"
        type="number"
      ></v-text-field>

      <v-text-field
        v-model="form.price"
        label="Price per Pax"
        type="number"
      ></v-text-field>

      <v-btn v-if="form.id" class="me-4" @click="handleSubmit(form.id)">
        submit
      </v-btn>
      <v-btn v-else class="me-4" @click="handleSubmit('')"> submit </v-btn>

      <v-btn @click="handleReset"> clear </v-btn>
    </form>

    <v-table class="mt-10">
      <thead>
        <tr>
          <th class="text-left">Tour Name Indonesia</th>
          <th class="text-left">Tour Name English</th>
          <th class="text-left">Destination</th>
          <th class="text-left">Total QTY</th>
          <th class="text-left">Price per Pax</th>
          <th class="text-left" :style="{ minWidth: '250px' }"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in listItem" :key="index">
          <td>{{ item.product_name_id }}</td>
          <td>{{ item.product_name_en }}</td>
          <td>{{ item.destination }}</td>
          <td>{{ item.qty }}</td>
          <td>{{ item.price }}</td>
          <td>
            <v-btn
              class="mr-2"
              append-icon="mdi-pencil"
              variant="outlined"
              @click="handleEdit(item)"
            >
              Edit
            </v-btn>

            <v-btn
              append-icon="mdi-trash-can"
              variant="outlined"
              @click="handleDelete(index)"
            >
              Delete
            </v-btn>
          </td>
        </tr>
      </tbody>
    </v-table>
  </v-container>
</template>

<script setup>
import { ref, reactive, computed } from "vue";

const destination = reactive([
  {
    id: 1,
    name: "Bali",
  },
  {
    id: 2,
    name: "Malang",
  },
  {
    id: 3,
    name: "Bandung",
  },
  {
    id: 4,
    name: "Jogja",
  },
]);

const form = ref({
  product_name_id: "",
  product_name_en: "",
  destination: 1,
  description: "",
  qty: 0,
  price: 0,
});

const listItem = reactive([
  {
    product_name_id: "Liburan Privat",
    product_name_en: "Private Holiday",
    destination: 1,
    description: "5 days with 10 destination",
    qty: "100",
    price: "3750000",
    id: 1,
  },
  {
    product_name_id: "Bersepeda Borobudur",
    product_name_en: "Cycling in Borobudur",
    destination: 2,
    description: "1 time purchase",
    qty: "40",
    price: "850000",
    id: 2,
  },
]);

const handleSubmit = (dataId) => {
  const playload = {
    product_name_id: form.value.product_name_id,
    product_name_en: form.value.product_name_en,
    destination: form.value.destination,
    description: form.value.description,
    qty: form.value.qty,
    price: form.value.price,
    id: dataId ? dataId : listItem.length + 1,
  };

  if (dataId) {
    listItem.map((item, index) => {
      if (item.id === dataId) {
        listItem[index] = playload;
      }
    });
  } else {
    listItem.push(playload);
  }
  handleReset();
};

const handleEdit = (playload) => {
  form.value = {...playload};
};

const handleDelete = (index) => {
  listItem.splice(index, 1);
};

const handleReset = () => {
  form.value = {
    product_name_id: "",
    product_name_en: "",
    destination: 2,
    description: "",
    qty: 0,
    price: 0,
  };
};
</script>
