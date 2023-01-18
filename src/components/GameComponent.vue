<template>
    <div class="garden">
      <div class="the-game">
        <div class="grid">
          <div class="square" v-for="(item,i) in minesweeper" :id="`${i+1}-square`" :class="{'bomb' : this.listOfBombs.includes(i+1)}" :key="i" @click="click(i+1)" @contextmenu.prevent="addFlag($event)">
              {{ !isNaN(item) ? item : '' }}
          </div>
        </div>
      </div>
    </div>
    <div class="result" >
          <div v-if="isGameOver">
              <span v-if="win">Hai Vinto!</span>
              <span v-else>Hai Perso!</span> <br>
              <button class="btn btn-danger" @click="retry()">Riprova!</button>
          </div>
      </div>
  </template>
  
  <script>
    export default {
        name: 'GameComponent',
      data(){
        return{
          numCell: 100,
          numBombs: 16,
          listOfBombs: [],
          minesweeper: [],
          privateCounter:0,
          isGameOver : false,
          win: false,
          counterFlag : 0
        }
      },
      methods:{
        getListBombs(){
          while(this.listOfBombs.length < this.numBombs){
          const random = Math.floor(Math.random() * this.numCell) + 1;
          if(!this.listOfBombs.includes(random)){
              this.listOfBombs.push(random);
            } 
          }
        //   console.log(this.listOfBombs);
        },
        buildMinesweeper(){
          for(let i=1; i<=this.numCell;i++){
            if(this.listOfBombs.includes(i)){
              this.minesweeper.push('x')
            }else{
              this.minesweeper.push('')
            }
          }
        },
        placeCounter(){
          const columns = Math.sqrt(this.numCell)
        for(let j = 0; j < this.listOfBombs.length; j++){
            const currentPosition = this.listOfBombs[j];
            const isRight = (currentPosition % columns === 0);
            const isLeft = (currentPosition % columns === 1);
            //in base alla posizione della cella imposto le condizioni da rispettare per andare a controllare una cella vicina
  
            if(!isLeft && currentPosition > columns) {
                const newPosition = currentPosition - columns -1;
                if(!this.listOfBombs.includes(newPosition)){
                    let counterBombs = parseInt(this.minesweeper[newPosition - 1]);
                    if(isNaN(counterBombs)){
                        counterBombs = 0;
                    }
                    counterBombs++;
                    this.minesweeper[newPosition - 1] = counterBombs;
                }
            }
            if(currentPosition > columns){
                const newPosition = currentPosition - columns;
                if(!this.listOfBombs.includes(newPosition)){
                    let counterBombs = parseInt(this.minesweeper[newPosition - 1]);
                    if(isNaN(counterBombs)){
                        counterBombs = 0;
                    }
                    counterBombs++;
                    this.minesweeper[newPosition - 1] = counterBombs;
                }
            }
            if(!isRight && currentPosition > columns){
                const newPosition = currentPosition - columns + 1;
                if(!this.listOfBombs.includes(newPosition)){
                    let counterBombs = parseInt(this.minesweeper[newPosition - 1]);
                    if(isNaN(counterBombs)){
                        counterBombs = 0;
                    }
                    counterBombs++;
                    this.minesweeper[newPosition - 1] = counterBombs;
                };
            }
            if(!isLeft && currentPosition > 0){
                const newPosition = currentPosition - 1;
                if(!this.listOfBombs.includes(newPosition)){
                    let counterBombs = parseInt(this.minesweeper[newPosition - 1]);
                    if(isNaN(counterBombs)){
                        counterBombs = 0;
                    }
                    counterBombs++;
                    this.minesweeper[newPosition - 1] = counterBombs;
                }
            }
            if(!isRight && currentPosition > 0){
                const newPosition = currentPosition + 1;
                if(!this.listOfBombs.includes(newPosition)){
                    let counterBombs = parseInt(this.minesweeper[newPosition - 1]);
                    if(isNaN(counterBombs)){
                        counterBombs = 0;
                    }
                    counterBombs++;
                    this.minesweeper[newPosition - 1] = counterBombs;
                }
            }
            if(!isLeft && currentPosition <= (this.numCell - columns)) {
                const newPosition = currentPosition + columns -1;
                if(!this.listOfBombs.includes(newPosition)){
                    let counterBombs = parseInt(this.minesweeper[newPosition - 1]);
                    if(isNaN(counterBombs)){
                        counterBombs = 0;
                    }
                    counterBombs++;
                    this.minesweeper[newPosition - 1] = counterBombs;
                }
            }
            if(currentPosition <= (this.numCell - columns)){
                const newPosition = currentPosition + columns;
                if(!this.listOfBombs.includes(newPosition)){
                    let counterBombs = parseInt(this.minesweeper[newPosition - 1]);
                    if(isNaN(counterBombs)){
                        counterBombs = 0;
                    }
                    counterBombs++;
                    this.minesweeper[newPosition - 1] = counterBombs;
                }
            }
            if(!isRight && currentPosition <= (this.numCell - columns)){
                const newPosition = currentPosition + columns + 1;
                if(!this.listOfBombs.includes(newPosition)){
                    let counterBombs = parseInt(this.minesweeper[newPosition - 1]);
                    if(isNaN(counterBombs)){
                        counterBombs = 0;
                    }
                    counterBombs++;
                    this.minesweeper[newPosition - 1] = counterBombs;
                }
            }
          }
  
        },
        click(numb)
          {   
              const columns = Math.sqrt(this.numCell)
              let cell = document.getElementById(`${numb}-square`)
              if(this.isGameOver) return;
              if(cell.classList.contains('flag')) return;
              if(cell.classList.contains('checked')) return;
              if(cell.classList.contains('show')) return;
              const currentPosition = parseInt(cell.id);
              if (this.listOfBombs.includes(currentPosition)){
                //   console.log(cell);
                  this.gameOver(0);
              }else{
                  //al click rendo la cella cliccata 
                  cell.classList.add('checked');
                  //incremento il contatore dei click
                  this.privateCounter++;
                  //condizione di vittoria
                  if (this.privateCounter == (this.numCell-this.numBombs)){
                      return this.gameOver(1);
                  }
                  let closerBombsCounter = parseInt(cell.textContent);
                  //se ha una bomba vicino fermo il controllo delle celle vicine
                  if(!isNaN(closerBombsCounter)){
                      return;
                  }
                  //se invece non ci sono bombe vicine controllo tutte le posizioni vicine
                  //valori booleani per indicare se la cella è a destra o sinistra
                  const isRight = (currentPosition % columns === 0);
                  const isLeft = (currentPosition % columns === 1);
                  //in base alla posizione della cella imposto le condizioni da rispettare per andare a controllare una cella vicina
                  setTimeout(()=>{
                      if(!isLeft && currentPosition > columns) {
                          const newPosition = currentPosition - columns -1;
                          this.click(newPosition);
                      }
                      if(currentPosition > columns){
                          const newPosition = currentPosition - columns;
                          this.click(newPosition);
                      }
                      if(!isRight && currentPosition > columns){
                          const newPosition = currentPosition - columns + 1;
                          this.click(newPosition);
                      }
                      if(!isLeft && currentPosition > 0){
                          const newPosition = currentPosition - 1;
                          this.click(newPosition);
                      }
                      if(!isRight && currentPosition > 0){
                          const newPosition = currentPosition + 1;
                          this.click(newPosition);
                      }
                      if(!isLeft && currentPosition <= (this.numCell - columns)) {
                          const newPosition = currentPosition + columns -1;
                          this.click(newPosition);
                      }
                      if(currentPosition <= (this.numCell - columns)){
                          const newPosition = currentPosition + columns;
                          this.click(newPosition);
                      }
                      if(!isRight && currentPosition <= (this.numCell - columns)){
                          const newPosition = currentPosition + columns + 1;
                          this.click(newPosition);
                      }
                  },10);
              }
          },
          gameOver(vinto)
      {   
          this.isGameOver = true;
          let arraySquares = document.getElementsByClassName('square')
          //printo il messaggio di vittoria o sconfitta
          if (vinto){
              //aggiungo ad ogni elemento bomba la classe che mette la flag mostro le altre caselle non cliccate
              for (let i = 0; i < arraySquares.length; i++){
                  if(arraySquares[i].classList.contains('bomb')){
                      arraySquares[i].classList.add('flag');
                  }else{
                      arraySquares[i].classList.add('show');
                  }
              }
              this.win = true;
          }else{
              //aggiungo ad ogni elemento bomba la classe che la evidenzi e mostro le altre caselle non cliccate
              for (let i = 0; i < arraySquares.length; i++){
                  if(arraySquares[i].classList.contains('bomb')){
                      arraySquares[i].classList.add('bomb-exploded');
                  }else{
                      arraySquares[i].classList.add('show');
                  }
              }
              this.win = false;
          }
      },
      addFlag(e){
          let cell = e.target;
          if(this.isGameOver) return;
          if(cell.classList.contains('flag')){
              this.counterFlag--;
              cell.classList.remove('flag');
              return;
          }
          if(this.counterFlag >= this.numBombs) return;
          if(cell.classList.contains('checked')) return;
          this.counterFlag++;
          cell.classList.add('flag');
      },
      retry(){
            let squares = document.getElementsByClassName('square');
            for(let i=0; i<squares.length; i++){
                squares[i].className = 'square';
            }
            this.listOfBombs = [];
            this.minesweeper = [];
            this.privateCounter = 0;
            this.isGameOver = false;
            this.win= false;
            this.counterFlag = 0;
            this.getListBombs();
            this.buildMinesweeper();
            this.placeCounter();
      }
      },
      mounted(){
        this.getListBombs();
        this.buildMinesweeper();
        this.placeCounter();

      }
    }
  </script>
  
  <style lang="scss" scoped>
  .garden{
    display: flex;
    justify-content: center;
    align-items: center;
  }
  /******************** classi del gioco ***********************************/
  
  .the-game{
      display: flex;
      justify-content: center;
      align-items: center;
      padding-top: 2rem;
      height: 550px;
  }
  .grid{
      width: 500px;
      height: 500px;
      display: flex;
      flex-wrap: wrap;
      justify-content: flex-start;
  }
  .square{
      width: 10%;
      height: 10%;
      border: 5px outset lightgrey;
      background-color: grey;
      color: transparent;
      display: flex;
      justify-content: center;
      align-items: center;
      font-weight: bold;
      font-size: 18px;
      cursor: pointer;
  }
  /******************** debug ***********************************/
//   .bomb{
//       background-color: red;
//   }
  /******************** debug ***********************************/
  
  .show{
      background-color: lightgrey;
      color: blue;
      border: 2px solid black;
  }
  .checked{
      background-color: white;
      color: blue;
      border: 2px solid black;
  
  }
  .bomb-exploded{
      border: 2px solid black;
      background-color: rgb(240, 240, 13);
      background-image: url('/img/circle-radiation-solid.svg');
      background-size: contain;
      background-repeat: no-repeat;
      background-position: center;
  }
  .flag{
      border: 5px outset lightgrey;
      background-color: grey;
      background-image: url('/img/flag-solid.svg');
      background-size: 60% 60%;
      background-repeat: no-repeat;
      background-position: center;
  }
  .result{
    text-align: center;
      font-weight: bold;
      font-size: 2rem;
      padding-bottom: 1rem;
      height: 150px;
  }
  #difficulty{
      padding: 0.5rem 2rem;
      border-radius: 15px;
      background-color: white;
  }
  #btn{
      background-color: white;
      padding: 0.5rem 2rem;
      border-radius: 25px;
  }
  .red{
      background-color: red;
  }
  </style>