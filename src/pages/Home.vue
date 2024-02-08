<script >
  import {state} from '../state.js'
  import axios from 'axios';

  export default {
   

    data(){
        return{     
            state,
        }
    },
    created(){
        axios.get(state.baseUrl + 'api/setting', {}).then(response=> this.state.setting = response.data.results );
   
        this.state.actvPage = 1;
    }

  }
</script>

<template>
  <div class="bg-home">

    <div class="home">
        <div class="home-left">
            <img src="../assets/img/sushibac.png" alt="" class="sushi">
        </div>
        <div class="home-right ">
            <h1>SCOPRI LA VERA CUCINA ORIENTALE E PROVA IL NOSTRO SUSHI</h1>
            <p>SOLO SUL NOSTRO SITO UFFICIALE PUOI TROVARE IL NOSTRO MENU, PRENOTARE UN TAVOLO O ADDIRITTURA PRENOTARE IL
                TUO ASPORTO</p>
            <router-link :to="{ name: 'menu' }" class="btn shadow">Menu</router-link>

        </div>
    </div>

    <div class="home-respo">
        <div class="main">
            <h1>SCOPRI LA VERA CUCINA ORIENTALE E PROVA IL NOSTRO SUSHI</h1>
            <img src="../assets/img/sushibac.png" alt="" class="sushi-respo">
            <p>SOLO SUL NOSTRO SITO UFFICILAE PUOI TROVARE IL NOSTRO MENU, PERNOTARE UN TAVOLA O ADDIRITTURARA PRENOTARE IL
                TUO ASPORTO</p>
            <router-link :to="{ name: 'menu' }" class="btn shadow">Menu</router-link>
        </div>
    </div>
</div>
</template>

<style scoped lang="scss">
@use '../assets/styles/general.scss' as *;

* {
    font-family: 'Gabarito', cursive;
}

.main-home::-webkit-scrollbar {

    width: 10px;
    height: 10px;

}

.main-home::-webkit-scrollbar-thumb {
    border-radius: 20px;
    background: $c-header;

}

.main-home::-webkit-scrollbar-track {
    border-radius: 20px;
    background: rgba(52, 4, 7, 0.786);

}

.main-home::-webkit-scrollbar-thumb:hover {
    border-radius: 20px;
    background-color: $c-nav-link;
    border: 2px solid $c-header;

}
.home-respo{
    display: none;
    overflow: auto;
    
}
.bg-home{
    background-color: $c-background;
    width: 100vw;
    height: calc(100vh - 230px);
    position: fixed;
    left: 0;
    bottom: 0px;
    overflow: auto;
}
.home {
    margin: 0 auto;
    padding: 5rem;
    display: flex;
    

    .home-left {
        display: flex;
        align-items: flex-start;
        justify-content: flex-end;
        width: 50%;
        position: relative;
        .sushi {
            max-width: 700px;
        }

       

    }

    .home-right {
        font-size: 23px;
        width: 40%;
        height: 70%;
        
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        gap: 60px;

        p {
            width: 70%;
            align-self: flex-end;
            font-size: 20px;
        }

        .btn {
            width: 200px;
            padding: 20px 0;
            border-radius: 50px;
            display: flex;
            justify-content: center;
            align-self: center;
            font-size: 25px;
            background-color: #523333;
            border: 5px solid white;
        }
    }

}


@media (max-width: 1300px) {

    .bg-home{
        height: calc(100vh - 150px);
    }
    .home{
        display: none;
    }
    .home-respo{
        display: block;
        padding: 7.1rem 3rem;
        .main{
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: 20px;
            img{
                max-width: 700px;
            }
            .btn {
            width: 200px;
            padding: 15px 0;
            border-radius: 50px;
            display: flex;
            justify-content: center;
            align-self: center;
            font-size: 25px;
            background-color: #523333;
            border: 5px solid white;
            }
        }
    }
}

@media (max-width: 1200px){
    .home-respo{
        .main{
            gap: 23px;
            img{
                max-width: 600px;
            }
        }
    }
}
@media (max-width: 670px){
    .home-respo{
        
        .main{
            gap: 23px;
            img{
                max-width: 500px;
            }
        }
    }
}
@media (max-width: 470px){
    .home-respo{
        overflow-x: hidden;
        .main{
            gap: 26px;
            width: 100%;
            img{
                max-width: 350px;
            }
        }
    }
}
@media (max-width: 370px) {
    .home-respo{
        .main{
            gap: 35px;
            img{
                max-width: 300px;
            }
            h1{
                font-size: 27px;
            }
            p{
                font-size: 15px;
            }
        }
        .btn {
            width: 150px!important;
            padding: 10px 0;
            border-radius: 50px;
            display: flex;
            justify-content: center;
            align-self: center;
            font-size: 20px!important;
            background-color: #523333;
            border: 5px solid white;
            }
    }
}
</style>
