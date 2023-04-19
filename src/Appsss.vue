<template>
  <div>
    <h1>Lista de Usuários</h1>
    <button @click="novoUsuario">Novo Usuário</button>
    <table>
      <thead>
        <tr>
          <th>Nome</th>
          <th>E-mail</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(usuario, index) in usuarios" :key="usuario.id">
          <td>{{ usuario.nome }}</td>
          <td>{{ usuario.email }}</td>
          <td>
            <button @click="verUsuario(index)">Ver</button>
            <button @click="editarUsuario(index)">Editar</button>
            <button @click="excluirUsuario(index)">Excluir</button>
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="mostrarUsuario">
      <h2>{{ usuarioSelecionado.nome }}</h2>
      <p>E-mail: {{ usuarioSelecionado.email }}</p>
      <button @click="fecharModal">Fechar</button>
    </div>
    <div v-if="mostrarFormulario">
      <h2>{{ formularioTitulo }}</h2>
      <form @submit.prevent="salvarUsuario">
        <label>Nome:</label>
        <input type="text" v-model="usuarioSelecionado.nome" required>
        <label>E-mail:</label>
        <input type="email" v-model="usuarioSelecionado.email" required>
        <button>{{ formularioBotao }}</button>
        <button @click="fecharFormulario">Cancelar</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      usuarios: [
        { id: 1, nome: 'João', email: 'joao@mail.com' },
        { id: 2, nome: 'Maria', email: 'maria@mail.com' },
        { id: 3, nome: 'Pedro', email: 'pedro@mail.com' }
      ],
      mostrarUsuario: false,
      mostrarFormulario: false,
      usuarioSelecionado: { id: null, nome: '', email: '' },
      formularioTitulo: '',
      formularioBotao: ''
    };
  },
  methods: {
    novoUsuario() {
      this.usuarioSelecionado = { id: null, nome: '', email: '' };
      this.formularioTitulo = 'Novo Usuário';
      this.formularioBotao = 'Adicionar';
      this.mostrarFormulario = true;
    },
    editarUsuario(index) {
      this.usuarioSelecionado = Object.assign({}, this.usuarios[index]);
      this.formularioTitulo = 'Editar Usuário';
      this.formularioBotao = 'Salvar';
      this.mostrarFormulario = true;
    },
  excluirUsuario(index) {
    if (confirm('Deseja realmente excluir este usuário?')) {
    this.usuarios.splice(index, 1);
    }
  },
  verUsuario(index) {
    this.usuarioSelecionado = this.usuarios[index];
    this.mostrarUsuario = true;
  },
  fecharModal() {
    this.mostrarUsuario = false;
    },
  fecharFormulario() {
    this.mostrarFormulario = false;
    },
  salvarUsuario() {
    if (this.usuarioSelecionado.id) {
    // Edição de usuário existente
    const index = this.usuarios.findIndex(u => u.id === this.usuarioSelecionado.id);
    this.usuarios.splice(index, 1, this.usuarioSelecionado);
  } else {
  // Adição de novo usuário
    this.usuarioSelecionado.id = Date.now();
    this.usuarios.push(this.usuarioSelecionado);
    }
  this.fecharFormulario();
  }
  }
  };
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

table td, table th {
  border: 1px solid #ddd;
  padding: 8px;
}

table th {
  background-color: #f2f2f2;
}

button {
  margin-right: 10px;
}
</style>