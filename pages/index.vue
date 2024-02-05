<script setup>

const contactManager = reactive(new ContactManager());

function ContactManager() {
  return {
    contacts: [
      {
        id: 1,
        name: "Gagan",
        age: 30,
        gender: "Male",
        dateOfJoining: "2022-01-01",
        designation: "Developer",
        email: "Gagan@gmail.com",
      },
      {
        id: 2,
        name: "Hari",
        age: 28,
        gender: "Male",
        dateOfJoining: "2022-02-01",
        designation: "Designer",
        email: "Hari@gmail.com",
      },
    ],
    newContact: {
      name: "",
      age: null,
      gender: "",
      dateOfJoining: "",
      designation: "",
      email: "",
    },

    addContact() {
      if (
        this.newContact.name &&
        this.newContact.age &&
        this.newContact.gender &&
        this.newContact.dateOfJoining &&
        this.newContact.designation &&
        this.newContact.email
      ) {
        this.contacts.push({
          ...this.newContact,
          id: this.contacts.length + 1,
        });
        this.newContact.name = "";
        this.newContact.age = null;
        this.newContact.gender = "";
        this.newContact.dateOfJoining = "";
        this.newContact.designation = "";
        this.newContact.email = "";
      }
    },

    removeContact(id) {
      const index = this.contacts.findIndex((contact) => contact.id === id);
      if (index !== -1) {
        this.contacts.splice(index, 1);
      }
    },
  };
}
</script>

<template>
  <div class="container mx-auto p-8">
    <h1 class="text-3xl font-bold mb-8">Contact Manager</h1>

    <form @submit.prevent="contactManager.addContact">
      <label for="name" class="block mb-2">Name:</label>
      <input
        v-model="contactManager.newContact.name"
        type="text"
        id="name"
        class="border p-2 mb-4"
        required
      />

      <label for="age" class="block mb-2">Age:</label>
      <input
        v-model="contactManager.newContact.age"
        type="number"
        id="age"
        class="border p-2 mb-4"
        required
      />

      <label for="gender" class="block mb-2">Gender:</label>
      <select
        v-model="contactManager.newContact.gender"
        id="gender"
        class="border p-2 mb-4"
        required
      >
        <option value="">Select Gender</option>
        <option value="Male">Male</option>
        <option value="Female">Female</option>
        <option value="Other">Other</option>
      </select>

      <label for="dateOfJoining" class="block mb-2">Date of Joining:</label>
      <input
        v-model="contactManager.newContact.dateOfJoining"
        type="date"
        id="dateOfJoining"
        class="border p-2 mb-4"
        required
      />

      <label for="designation" class="block mb-2">Designation:</label>
      <input
        v-model="contactManager.newContact.designation"
        type="text"
        id="designation"
        class="border p-2 mb-4"
        required
      />

      <label for="email" class="block mb-2">Email:</label>
      <input
        v-model="contactManager.newContact.email"
        type="email"
        id="email"
        class="border p-2 mb-4"
        required
      />

      <button
        type="submit"
        class="bg-teal-500 text-white font-bold py-2 px-4 rounded"
      >
        Add Employee
      </button>
    </form>

    <ul class="mt-8">
      <li
        v-for="contact in contactManager.contacts"
        :key="contact.id"
        class="mb-4"
      >
        <div class="flex justify-between items-center">
          <div>
            <p>Name:{{ contact.name }}</p>
            <p>Age: {{ contact.age }}</p>
            <p>Gender: {{ contact.gender }}</p>
            <p>Date of Joining: {{ contact.dateOfJoining }}</p>
            <p>Designation: {{ contact.designation }}</p>
            <p>Email: {{ contact.email }}</p>
          </div>
          <button
            @click="contactManager.removeContact(contact.id)"
            class="text-red-500"
          >
            Remove
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
