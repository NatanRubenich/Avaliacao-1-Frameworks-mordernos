<!--Na avaliação 1 construa um App com VUE 3 CLI utilizando o conhecimento adquirido na unidade 1. Os requisitos são:

Entender o framewok Vue, seu Lifecyle e instância;
Utilizar o restorno de data para instância vue contendo variáveis a serem utilziadas pelo app;
Utilizar métodos;
Utilizar V-IF, V-ELSE, V-FOR;
V-BIND, V-ON, V-MODEL, V-SHOW;

Aluno: Natan Rübenich
Professor: Ivan Pires
Disciplina: 

O que fiz: Uma aplicação simples e bonita, que adiciona em uma lista para 
-->

<template>
  <div id="app">
    <h1>{{ titulo }}</h1>
    <!-- V-IF para mostrar a string na variávei quando clicado aí-->
    <p v-if="mostrar_mensagem">{{ mensagem }}</p>
    <!-- Mesma coisa do V-if mas o oposto aí -->
    <p v-else>Nenhum item adicionado ainda.</p>
    <ul>
      <!--  V-FOR para listar o que foi inputado aí -->
      <li v-for="(item, index) in items" :key="index">{{ item }}</li>
    </ul>
    <!-- V-MODEL para ligação bidirecional de dados ao input -->
    <input v-model="imputar_valor" @keyup.enter="adicionar_item" />
    <button @click="adicionar_item" :disabled="imputar_valor === ''">Adicionar algo</button>
    <div v-bind:class="{ 'destaque': destacado }">
      <!-- V-SHOW para renderização condicional de um elemento com display: none -->
      <p v-show="mostrar_texto">{{ texto }}</p>
      <!-- V-ON para vincular um evento a um método -->
      <button v-on:click="destacar">Destacar texto</button>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      titulo: "Minha lista de alguma coisa",
      mensagem: "O botão foi clicado :D",
      mostrar_mensagem: false,
      imputar_valor: "",
      items: [],
      texto: "Ao clicar, vai destacar o texto :D",
      mostrar_texto: true,
      destacado: false
    };
  },
  methods: {
    adicionar_item() {
      if (this.imputar_valor !== "") {
        this.items.push(this.imputar_valor);
        this.imputar_valor = "";
        this.mostrar_mensagem = true;
      }
    },
    destacar() {
      this.destacado = !this.destacado;
    }
  }
};
</script>


<style>
/* perfumarias e outras cosias para deixar bonitinho aí */ 
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #f5f5f5;
  font-family: Arial, sans-serif;
}

h1 {
  font-size: 3rem;
  margin-bottom: 2rem;
  text-align: center;
}

p {
  font-size: 1.2rem;
  margin-bottom: 2rem;
  text-align: center;
  color: #333;
}

ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

li {
  font-size: 1.2rem;
  margin-bottom: 1rem;
  color: #333;
}

input {
  font-size: 1.2rem;
  padding: 0.5rem;
  border: none;
  border-radius: 0.25rem;
  margin-bottom: 1rem;
}

button {
  font-size: 1.2rem;
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 0.25rem;
  background-color: #333;
  color: #fff;
  cursor: pointer;
}

.destaque {
  border: 2px solid rgb(0, 0, 0);
  padding: 1rem;
  margin-top: 2rem;
}

/* 
Esse codigo tem a autenticação e certificação GO HORSE de qualidade https://www.gohorsecertification.com.br

                                                                                                                                                      
                                                                                ::                                                                    
                                                                                ++                                                                    
                                                                                ++                                                                    
                                                                      ..--      ::                                                                    
                                                                      ++..      --      ::                                                            
                            ::                                        mm      ..    ::::  ::::                                                        
                          ++            ::::                          mm      --    ::      ::            ++::                                        
                        ++            ::    ::                        mm--    ++  ..        ::          ++  mm                                        
                      ++            ++        ::                      ++      ++  --        --        ++    ++            ::                          
                    ::              ::        ::                      ::      ++            ::      --..  ..--          ++                            
                    --              ::                    ::::::::::  --      ::    --      ::      mm::++--      ::::++          ++++--              
                  ..                mm          ::    ++--                    ++          ::        mm            ++            ++    ..::            
                  ::        mmmm::  ++        ::--++                                              ::--::          mm          --                      
                  ++      ++    --    ::++++mm++              ::++++::::::::++++++::--            ++  ++            ++        ++                      
                  ++            --        ++            ++++                          ::++--            ::++        ++      --++::::                  
                  --            ::    ++..          ++..                                    ++++            ::              ++                        
                    ++--      ++  --::          ::::                                            ::++          ::::  ....    ::                        
                        ::++::  ++            ++..    ::::::++::::::--::::::::::::--                  mm--                ::                          
                              ::            ::  ::::                                  ::--              --++..            MM--                        
                            ++            ..mm                                            --..              ..::              ::::--                  
                          ++            ::++                                                  ::                ::::                                  
                        ::..          ++                                                        ++                  ++::                              
                      ++--          ++                                                            ----                  ++                            
                    --++          ::                        mm::                                      ++                  ++                          
                    ++          ::                        ::++++                                        ++                  ++..                      
                  ++..        ::                          ::::  ::                                        ::..                ++                      
                ..++        ::                            --    ++                                            ::                ++..                  
                ++          --                            ..    --                                              ::                ++                  
              ..::        ::                                                ::::::                                ++                mm                
              ::          ::                                                      ..                                ++                ::              
            --::                                        ..                    --..::::                                ++              mm              
          ++::..        ..                              --                    ::++::++                                  ++..            mm            
          ++::          --                              ::                ++  ++..MM++  --....------..                    ++            ::            
          ++::          ::::                            ::                      ::++::                          ..  ----++::mm            mm          
        --::            ::                                --                                                      --  --    ::mm          --..        
        ++::          --::                                ::                                                      --##++      ++--          ++        
        mm::          ::::                                  ..                                                      ++--        mm          ++        
        mm--          mm                                                                                                        mm          --        
        MM            MM                                                                                                      ..++            ..      
      mmMM            mm                                  --  --                                                  ++++        ..::::          ::      
      MMMM            ++                                  mmmm                                                        ++MMmm++--::::          ++      
      @@@@          ::::                      --++mm++++++MM++                                                                  --::          ++      
    ..@@MM          mm++                ::++++--..++++++++mm                                                      ::::::        ----          --      
    ::@@MM          MM::                ::--::mm::::mm++--MM                                                ::++::              ----          --      
    mmMMMM          MM--                  mm::::mm::--::::++                        ..++++++++++++++++++++..                      ::          ..      
    MMmmmm          MM--::              mm::mm--..::++--::--                        ++                                            ++          --      
    mmMMmm::        mm--::              ++++--::++--++::mm                          ++                                            ::          ..      
    ++@@MM::        mm----                  ++--++::--::MM                        mm++                                            ::          --      
    ..MMMM::        ++------              ++++++--++--::mm                        ++mm                                            ::          --      
      MMmm++        ::----::            --++::++--::::++++                          ++                                          ....          ::      
      ::mmMM        ::::--::            mm::    ++----mm++                          ++::                                        --            --      
        mm++          mm--::          ::    ::::--++++::::                          mm++                                        ++            ..      
        ++mm::        mm--::              ++::::--  mm++                            mm::                                        mm                    
          MMmm        ..::--            ::..      ++MM                              ::++                                        mm          ::        
          @@mm::        mm--                ..++::::mm                                mm::                                      ++          ::        
          ++@@++        mm..::          ::::      MM                                  mm++                                      ::                    
            @@++..      ..::::                ::++++                                  ++mm                                    --          --          
            MM++++        mm----            mm::--mm                                    MM..                                  mm          --          
            --@@++          ++..          ::--..::++                                    mm::                                  --        --            
              @@++::        mm++        ..::..++mm                                      mmmm                                mm          --            
              ++MM++--        MM        ++++mm++mm                                        ::++                            ::          ::              
                @@mm::        ::..    ::mmMM--::..                                        ::MM                            ++        --                
                --MM--++        ++--  mm--    mm                                          ++mm                          ++          ::                
                  ++++++          ::++                                                    ..::::                    ::::          --                  
                  --++--::      ::mm                                                        ++mm                  ++..          --                    
                    ::mm++      ::  ++++                                                    ++                ++::              ..                    
                    ::--mm::        ::  --mm::--::::                                          ++          ::++                --                      
                      ::++MM          ++            --++++::                                  --      ++..                  ::                        
                      mm::::            ::                    --::++++++++++mm++++++++++::::::::                          ::                          
                        ++::                                                                                            ::                            
                        --::--                                                                                        ::                              
                          ::mm--                                                                                  --                                  
                            mmMM::                                                                              ::                                    
                      ::      ..MM++                                                                      ..::                                        
                    ++::++      ..MM..                                                                --::                                            
                    ++    ++      ..mm--                                                          ::--                                                
                  mm        --        ::::                                                  --::                                                      
                ++        ..::          ..::                                          --::..      ::                                                  
                ++        mm    ++++          ::::--                          ..::::..          mm                                                    
              mmmm++++++++    ++--++                    ::::::::::::::::::--                    mm                                                    
            ++              ++--::::                                                ..--        --++                                                  
          ::              --::++--                                        ++++::    ++            ++                                                  
                          mm              --++mm        ..::            ++          ::              ++                                                
                        mm              ++      --    ..::              mm::--      mm                ..                                              
                        ..::::::      ..        ..    ++                ++            ++              ..                                              
                                  --  ::      ++    ::                  ++            ::            ::                                                
                                      ++    ::      ++                  mm            ..        ++::--                                                
                                                    ++          ..::    ::::::..    --::                                                              
                                                    --::    ..++                                                                                      
                                                        ----                                                                                          
                                                                                                                                                      
*/
</style>