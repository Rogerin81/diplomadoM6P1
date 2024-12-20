<template>
  <div class="container mt-8">
    <h1 class="text-center mb-4">Gestión de Contactos</h1>

    <!-- Formulario para buscar -->
    <div class="mb-3">
      Filtra por:<input
        type="text"
        v-model="searchQuery"
        placeholder="nombre o correo"
        class="form-control"
      />
    </div>

    <!-- Tabla para mostrar contactos -->
     <div class="card mt-4">
    <table class="table table-striped">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nombre</th>
          <th>Correo</th>
          <th>Dirección</th>
          <th>Teléfono</th>
          <th>País</th>
          <th>Ciudad</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(contact, index) in filteredContacts" :key="contact.id">
          <td>{{ contact.id }}</td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.email }}</td>
          <td>{{ contact.address }}</td>
          <td>{{ contact.phone }}</td>
          <td>{{ contact.country }}</td>
          <td>{{ contact.city }}</td>
          <td>
            <button
              class="btn btn-info btn-sm me-1"
              @click="editContact(index)"
            >
              Editar
            </button>
            <button
              class="btn btn-danger btn-sm"
              @click="deleteContact(index)"
            >
              Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>
    </div>

    <!-- Formulario para agregar o editar -->
    <div class="card mt-4">
      <div class="card-body">
        <h3>{{ isEditing ? "Editar Contacto" : "Agregar Contacto" }}</h3>
        <form @submit.prevent="saveContact">
          <div class="mb-3">
            <input
              type="text"
              v-model="currentContact.name"
              placeholder="Nombre"
              class="form-control"
              required
            />
          </div>
          <div class="mb-3">
            <input
              type="email"
              v-model="currentContact.email"
              placeholder="Correo Electrónico"
              class="form-control"
              required
            />
          </div>
          <div class="mb-3">
            <input
              type="text"
              v-model="currentContact.address"
              placeholder="Dirección"
              class="form-control"
            />
          </div>
          <div class="mb-3">
            <input
              type="tel"
              v-model="currentContact.phone"
              placeholder="Teléfono"
              class="form-control"
            />
          </div>
          <div class="mb-3">
            <input
              type="text"
              v-model="currentContact.country"
              placeholder="País"
              class="form-control"
            />
          </div>
          <div class="mb-3">
            <input
              type="text"
              v-model="currentContact.city"
              placeholder="Ciudad"
              class="form-control"
            />
          </div>
          <button type="submit" class="btn btn-primary">
            {{ isEditing ? "Guardar Cambios" : "Agregar Contacto" }}
          </button>
          <button
            type="button"
            class="btn btn-secondary ms-2"
            @click="cancelEdit"
            v-if="isEditing"
          >
            Cancelar
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      contacts: [
        {
          id: 1,
          name: "Alice Johnson",
          email: "alice.johnson@example.com",
          address: "123 Maple Street",
          phone: "123-456-7890",
          country: "USA",
          city: "New York",
        },
        {
          id: 2,
          name: "Bob Smith",
          email: "bob.smith@example.com",
          address: "456 Oak Avenue",
          phone: "987-654-3210",
          country: "Canada",
          city: "Toronto",
        },
        {
          id: 3,
          name: "Carol White",
          email: "carol.white@example.com",
          address: "789 Pine Road",
          phone: "555-123-4567",
          country: "UK",
          city: "London",
        },
        {
          id: 4,
          name: "David Brown",
          email: "david.brown@example.com",
          address: "321 Elm Street",
          phone: "444-555-6666",
          country: "Australia",
          city: "Sydney",
        },
        {
          id: 5,
          name: "Emily Davis",
          email: "emily.davis@example.com",
          address: "654 Spruce Lane",
          phone: "333-444-5555",
          country: "USA",
          city: "Los Angeles",
        },
      ],
      searchQuery: "",
      currentContact: {
        id: null,
        name: "",
        email: "",
        address: "",
        phone: "",
        country: "",
        city: "",
      },
      isEditing: false,
    };
  },
  computed: {
    filteredContacts() {
      return this.contacts.filter(
        (contact) =>
          contact.name
            .toLowerCase()
            .includes(this.searchQuery.toLowerCase()) ||
          contact.email.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    saveContact() {
      if (this.isEditing) {
        const index = this.contacts.findIndex(
          (c) => c.id === this.currentContact.id
        );
        this.contacts.splice(index, 1, { ...this.currentContact });
      } else {
        const newId =
          this.contacts.length > 0
            ? Math.max(...this.contacts.map((c) => c.id)) + 1
            : 1;
        this.contacts.push({ ...this.currentContact, id: newId });
      }
      this.resetForm();
    },
    deleteContact(index) {
      if (confirm("¿Está seguro de eliminar este contacto?")) {
        this.contacts.splice(index, 1);
      }
    },
    editContact(index) {
      this.currentContact = { ...this.contacts[index] };
      this.isEditing = true;
    },
    cancelEdit() {
      this.resetForm();
    },
    resetForm() {
      this.currentContact = {
        id: null,
        name: "",
        email: "",
        address: "",
        phone: "",
        country: "",
        city: "",
      };
      this.isEditing = false;
    },
  },
};
</script>

<style>
.container {
  max-width: 800px;
  margin: auto;
  margin-top: 80px;
}
</style>
