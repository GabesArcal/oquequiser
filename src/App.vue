<script setup>

    import { ref } from 'vue'; // Essa funcão tornara o let reativo


    const cidade = "Ibaté"; //foi dado o nome de cidade para essa constante

    const produto = {
        nome: "Chokito tradicional",
        valor: 2.50,
        estoque: 12
    }

    // const contador = 0;  Não podemos usar "const" porque ela altera e a constante é constante
    let contador = ref(0); // Sempre que tiver uma variavel que você quer que mude na tela em tempo real você tem que declarar importando o "ref"
    // Aonde for reativo (tudo que for aparecer na hora)
    // const incrementa () => {} Essa const é a mesma coisa que function logo a baixo(porém é mais usado no BackEnd)

    let acesso = ref("usuario"); // O ref significa que o torna reativo a imagem, e apartir do momento que se torna reativo você precisa colocar .value no final

    function alterarAcesso(){
        if( acesso.value == "usuario"){
            acesso.value = "admin";
        }else{
            acesso.value = "usuario";
        }

        //acesso.value = "admin"; // Toda vez que uma funcão tiver que ser mostrada na hora é precido que não se esqueça de colocar o .value na "let" se não ira funcionar.
        //na linha de cima ele só mostra admin e faz a função ineficiente
    }

    function incrementaValor(numero){
       
        contador.value += numero
        // É preciso adicionar ".value" para que pegue a let reativa
        // alert("aumentou para "+contador+" !")

        if( contador.value <= 0 ){
            contador.value = 0   // Para "travar" e não deixar que passe do 0 foi preciso esse if falando que se for igual ou a 0 ele força 0, fazendo assim que a função não trave por conta do -1
        }

    }

    // function diminuirValor(){
    //     contador.value-- // É preciso adicionar ".value" para que pegue a let reativa
    // }

</script>

<template setup>

    <h1>Conradito Chokito</h1>
        <p>A melhor chocolateria de {{ cidade }} São Carlos e região!</p>
        <p>2+2 é igual a {{  2+2 }}</p>

        <hr/>
        <p>Você está logado como {{ acesso }} - <button v-on:click="alterarAcesso()">Trocar </button></p>
               
        <hr/>

     <div v-if="acesso == 'admin'"> <!-- o admin -->
        <!-- v-if="acesso < alterarAcesso"> também funciona não sei como -->
        <h2>Produto mais vendidos:</h2>

            <p>Nome: {{ produto.nome }}</p>
            <p>Preço: {{ produto.valor }}</p>
            <p>Quantidade em estoque: {{ produto.estoque }}</p>

            <p>Contador : {{ contador }}</p>
            <button v-on:click="incrementaValor( 1 )" >Aumentar</button> 
            <!-- Para aumentar ou diminuir o valor basta adicionar entre parametro o valor que deseja e para menos com "-n(numero aleatorio)"-->
            <button v-on:click="incrementaValor( -1 )" >Diminuir</button>
            <!-- <button onclick="">Aumentar</button> -->
            <!-- <button v-on:click="diminuirValor">Diminuir</button> -->

            <!-- o v-on é para quando tem um evento como um click-->

            <p v-if="contador < 5 && contador > 0 "> Atenção: o estoque está muito baixo! </p>
            <!-- Ele precisa entender que precisa ser menor que 5 e maior que 0 usando o &&  -->
            <!-- Ele abre um v-if pra você no meio do html e ele só vai aparecer na tela se o meu computador for >5 e se for falso ele nem mostra pra você-->
            <p v-if="contador <= 0 "> Alerta: produto fora de estoque</p>
    </div>
</template>

<style setup>

</style>
