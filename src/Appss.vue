<template>
  <div>
    <h2>Lista de Usuários</h2>
    <table>
      <thead>
        <tr>
          <th>Nome</th>
          <th>Email</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in users" :key="index">
          <td>{{ user.name }}</td>
          <td>{{ user.email }}</td>
          <td>
            <button @click="editUser(index)">Editar</button>
            <button @click="deleteUser(index)">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>

    <h2 v-if="selectedUser !== null">Editar Usuário</h2>
    <form v-if="selectedUser !== null" @submit.prevent="submitUserForm">
      <div>
        <label for="name">Nome:</label>
        <input type="text" id="name" v-model="selectedUser.name" required />
      </div>
      <div>
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="selectedUser.email" required />
      </div>
      <button type="submit">{{ selectedUser === null ? 'Criar' : 'Salvar' }}</button>
      <button type="button" @click="cancelEdit">Cancelar</button>
    </form>

    <button @click="createUser">Adicionar Usuário</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      users: [
        { name: 'João', email: 'joao@example.com' },
        { name: 'Maria', email: 'maria@example.com' },
        { name: 'Pedro', email: 'pedro@example.com' },
      ],
      selectedUser: null,
    };
  },
  methods: {
    createUser() {
      this.selectedUser = { name: '', email: '' };
    },
    editUser(index) {
      this.selectedUser = { ...this.users[index] };
    },
    deleteUser(index) {
      this.users.splice(index, 1);
    },
    submitUserForm() {
      if (this.selectedUser.name && this.selectedUser.email) {
        if (Object.prototype.hasOwnProperty.call(this.selectedUser, 'id')) {
          // atualiza usuário existente
          const index = this.users.findIndex(user => user.id === this.selectedUser.id);
          this.$set(this.users, index, this.selectedUser);
        } else {
          // cria novo usuário
          this.users.push({
            id: new Date().getTime(),
            name: this.selectedUser.name,
            email: this.selectedUser.email,
          });
        }
        this.selectedUser = null;
      }
    },
    cancelEdit() {
      this.selectedUser = null;
    },
  },
};
</script>

<style>
  table {
    width: 100%;
    border-collapse: collapse;
  }

  th, td {
    padding: 8px;
    border-bottom: 1px solid #ddd;
  }

  th {
    background-color: #f2f2f2;
    text-align: left;
  }

  form > div {
    margin-bottom: 16px;
  }

  label {
    display: inline-block;
    width: 100px;
  }

  input[type="text"], input[type="email"] {
    width: 100%;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
    box-sizing: border-box;
  }

  button[type="submit"], button[type="button"], button {
    background-color: #4CAF50;
    color: #fff;
    padding: 8px 16px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  button[type="submit"]:hover, button[type="button"]:hover, button:hover {
    background-color: #3e8e41;
  }

  button[type="submit"] {
    margin-right: 16px;
  }

  button[type="button"] {
    background-color: #f44336;
  }

  button[type="button"]:hover {
    background-color: #cc2d23;
  }
</style>