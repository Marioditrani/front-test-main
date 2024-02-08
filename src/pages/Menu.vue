<script >
  import {state} from '../state.js';
  import axios from 'axios'


  export default {
   

    data(){
        return{     
            state,
            arrProduct:[],
            arrCategory:[],
            categoryId: 0,
            actvcat: 1,
            catinput:0,
        }
    },
    methods:{
      namecategory(n,i){
        if(this.categoryId==0 && i==0){
          return'categorie'
        }
        i++
        if(this.categoryId==i && i!==0){
          return n
        }
      },
      catopen(){
        if (this.catinput){
          this.catinput = 0
        }else{
          this.catinput = 1
        }
        console.log(this.catinput)
      },
      getProduct(cat){
        this.categoryId = cat,
        axios
				.get(state.baseUrl + 'api/projects', {
					params: {
						category: this.categoryId,
					},
				})
				.then(response => {
          this.arrProduct = response.data.results.data;
				});
      },
      getCategory(){

        axios
				.get(state.baseUrl + 'api/categories', {})
				.then(response => {
          this.arrCategory = response.data.results;
				});
 
      },
      changeCategory(value){
        if(value==1){
          this.getProduct(0)
          this.actvcat=value
          
        }else{
          this.getProduct(value)
          this.actvcat=value

        }
      },
      getPrice(cent){
        let num = parseFloat(cent);
        num = num / 100;
        num = "€" + num  
        
        return num
      },
      fixtag(arr){
        let arrtag='';
        arr.forEach((element, i) => {
          
          if(i+1==arr.length){
            
            arrtag = arrtag + element.name + '.'
          }else{
            arrtag = arrtag + element.name + ', '
            
          }
        });
        return arrtag
      },
      
      
      
    },
    created(){
      this.getProduct(0);
      this.getCategory();


      this.state.actvPage = 2;
    },
    
  }
</script>

<template>
  <div class="menu">
    <div class="menu-cont">
      <div class="menu-left">
        <img src="../assets/img/crop.png" alt="" class="bac">
        
      </div>
      <div class="menu-right">
        <div class="menu-top">
          <div class="menu-top-left">
            <div class="menu-top-respo">
              <img src="../assets/img/crop.png" alt="" class="bac-respo">
              <h1>Menu</h1>
            </div>
            <p>Le delizie del nostro menu aspettano solo te...</p>
          </div>
          <div class="menu-top-right">
            <div class="one-category shadow" @click="catopen(catinput)" :class="catinput ? 'cat-off': 'cat-on'">
              <span v-for="(cat,i) in arrCategory" :key="i">{{ namecategory(cat.name, i)}}</span>
            </div>
            <div class="categorie"   :class="catinput ? 'cat-on': 'cat-off'">
              <div v-for="(cat, i) in arrCategory" class="category" :class="actvcat == cat.id ? 'category-on' : '', i == 0 ? 'category0' : '',i == 1 ? 'category1' : '', i == 2 ? 'category2' : '',i == 3 ? 'category3' : '',i == 4 ? 'category4' : '',i == 5 ? 'category5' : '',i == 6 ? 'category6' : '' " @click="changeCategory(cat.id)" :key="i"> 
                <span @click="catopen(catinput)" :class="actvcat == cat.id ? 'span-on' : '' ">{{ cat.name }}</span> 
              </div>
            </div>
          </div>
        </div>
        <div class="menu-bottom">

          <div class="card " v-for="item in arrProduct">
            <img  class="shadow" src="../assets/img/imgsushi.png" alt="">         <!--state.getImageUrl(item.image)-->
            <div class="c-tp shadow">
              <div class="title">{{ item.name }}</div>
              <div class="tags"> <span>{{fixtag(item.tags) }}</span></div>
              <div class="price">{{ getPrice(item.price) }}</div>
            </div>
          </div>
          
        </div>

      </div>
    </div>
    
  </div>
</template>

<style scoped lang="scss">
@use '../assets/styles/general.scss' as *;


.menu-cont::-webkit-scrollbar{
      
      width: 10px;
      height: 10px;
      
  }

.menu-cont::-webkit-scrollbar-thumb {
    border-radius: 20px;
    background: $c-header;
    
}
.menu-cont::-webkit-scrollbar-track {
    border-radius: 20px;
    background: rgba(52, 4, 7, 0.786);
    
}
.menu-cont::-webkit-scrollbar-thumb:hover {
    border-radius: 20px;
    background-color: $c-nav-link;
    border: 2px solid $c-header;
    
}
.hd{box-shadow: 10px 10px 10px black; }

.menu{
  width: 100%;
  overflow: hidden;
  display: flex;
  flex-direction:column;
  position: fixed;
  top: 0;
  left: 0;
  flex-wrap: wrap;
  height: 100vh;
  margin-top: 230px;
  
  .menu-cont{
    overflow: auto;
    display: flex;
    background-color: $c-background;
    width: 100%;
    padding: 1rem 1rem ;
    padding-bottom: 250px!important;
    overflow-x: hidden;
    .menu-left{
      width: 10%;
      display: flex;
      align-items: center;
      position: relative;
      
      .bac{
        width: 100%;
        margin: auto;
      }
      
    }

    .menu-right{
      width: 90%;
      .menu-top{
        
        display: flex;
        justify-content: space-between;
        h1{
          text-transform: uppercase;
          font-size: 80px;
          padding-top: 2rem;
        }
        p{
          font-size: 25px;
         
        }

        img{
          display: none;
        }
        
      }
      .menu-bottom{
      @include dfc;
      flex-wrap: wrap;
      gap: 1rem;
      align-items: stretch;
      padding-bottom: 300px;
      .card{
        border-radius: 10px;
        width: calc((75% - 2rem) / 3);
        padding: 10px;
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: center;
        margin: 15rem 1rem;
        margin-bottom:0 ;
        
        
        img{
          position: absolute;
          top: -130px;
          left: 0;
          right: 0;
          margin: auto;
          width: 250px;
          
          
        }
        .title{
          font-size: 20px;
          width: 100% ;
          text-transform: uppercase;
          z-index: 10001;
          
          
        }
        .c-tp{
          background-color: #AB2F2F;
          position: relative;
          z-index: 10000;
          display: flex;
          flex-direction: column;
          padding: 1rem 1.5rem;
          border-radius: 20px;
          justify-content: space-between;

          .tags, .price{
            border-radius: 10px;
            width: 100%;
            padding-bottom: .5rem;
          }
          .tags{

            display: flex;
            padding-top: 1rem;
            padding-right: .5rem;
            span{
              font-size: 13px;
              font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
              font-weight: bold!important; 


            }
          }
          .price{
            width: 100%;
            //border-radius: 10px ;
            text-align: right;
            padding-top: 0.5rem;
          }
        }
      }
      }
    }
    
    
    .main-menu{
      

    }
    
  }


}

/*** */
.one-category{
  background-color: #523333;
  width: 350px;
  
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  padding: 1.5em 1em;
  margin: 0 auto;
  z-index: 10;
  position: relative;
  border: 5px solid white;
  border-radius: 50px;
  margin: 40px ;
  span{
    font-size: 30px;
    
    text-align: center;
    transition: all .5s;
    text-transform: uppercase;
    
    letter-spacing: .1em;
  }
}
.categorie {
  box-shadow: -40px 50px 100px black ;
  background-color: #523333;
  max-width: 600px;
  width: 90%;
  height: 300px;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  gap: 5px;
  padding: 1.5em 1em;
  margin: 0 auto;
  z-index: 10;
  position: relative;
  border: 5px solid white;
  border-radius: 20px;
  .category {
   height: 100%;
   flex: 1;
   overflow: hidden;
   cursor:grab;
   border-radius: 2px;
   transition: all .5s;
   background-color: #D53C3C;
   display: flex;
   justify-content: center;
   align-items: center;
   span {
    min-width: 30em;
    padding: .5em;
    text-align: center;
    transition: all .5s;
    text-transform: uppercase;
    color: $c-nav-link;
    letter-spacing: .1em;
   }
  }

  .category0{
  background-color:rgba(213, 60, 60, 0.46);

}
.category1{
  background-color:rgba(213, 60, 60, 0.40);
}
.category2{
  background-color:rgba(213, 60, 60, 0.34);
}
.category3{
  background-color:rgba(213, 60, 60, 0.28);
}
.category4{
  background-color:rgba(213, 60, 60, 0.22);
}
.category5{
  background-color:rgba(213, 60, 60, 0.16);
}
.category6{
  background-color:rgba(213, 60, 60, 0.10);
}
.category-on {
  
  background-color: rgba(213, 60, 60,);
}
  .category:hover {
    
  }
  .category:hover span {
    color: white;
   transform: rotate(0);
  }
}

.category-on:hover {
  
  background-color: $c-header !important;
}
.span-on{
  color: white!important;;

}

.cat-off{display: none;}

/***** */



@media (max-width:$bp1) {
  .menu{
    width:100%;
  }
}
@media (max-width:1600px) {
  .card{
    width: calc((75% - 2rem) / 2)!important;
  }
}

@media (max-width: 1300px){
  .menu{
    margin-top:150px!important;
  }
}
@media (max-width:1100px) {
  
  .card{
    width: calc((100% - 2rem) / 2)!important;
  }
  .menu-cont{
    padding-top: 0!important;
  }
    .menu-top{
      flex-direction: column;
      align-items: center;
      .menu-top-left{
        padding: 2rem;
        padding-top: 0;
        
        h1{
          padding-top: 0!important;
          
        }
        
        .menu-top-respo{
          display: flex;
          align-items: center;
          justify-content: space-between;
          width: 80%;
          margin: auto;
        }
      }
    }
    
    
    .bac-respo{
      display: block!important;
      width: 100px;
      transform: rotateZ(120deg);
    }
    
    .card{
    margin-top: 20rem!important;
    width: 55% !important;
  }
  .menu-left{
    display: none!important;
  }
  .menu-right{
    width: 100%!important;
  }
}

@media (max-width:$bp2) {
  .menu-top-left{
    width: 100%;
    display: flex;
    flex-direction: column;
    .menu-top-respo{
      width: 100%!important;
      display: flex;
      justify-content: space-between;
      h1{
        font-size: 70px!important;
        
      }
  
      .bac-respo{
        width: 70px!important;
      }
    }
  }
  .menu-cont{
    width: 100%!important;
  }

  .card{
    
    width: 95% !important;
  }
}
@media (max-width:450px) {
  .menu-top-left{
    
    .menu-top-respo{
      padding-top: 3rem;
      text-align: center;
      
      
      h1{
        font-size: 60px!important;
      }
      .bac-respo{
        margin-right: 25px!important;
        width: 60px!important;
      }
      
    }
  }
  .one-category{
    width: 300px!important;
  }
  .categorie{
    max-width: 350px;
  }
  
}
</style>
