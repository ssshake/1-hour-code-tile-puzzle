<template>
  <div class="tile-container">
      <div class="tile" :class="value" @click="clicktile(key)" v-for="(value, key, index) in shuffledPieces" :key="index">
          <div v-if="value != 'empty'">
            <!-- {{value}} -->
          </div>
          <div v-else class="empty">
          </div>
      </div>
  </div>
</template>

<script>

import _ from 'lodash';

export default {
  name: 'HelloWorld',
  data() { 
      return {
        pieces: ["A", "B", "C", "D", "E", "F", "G", "H",  "empty"],
        shuffledPieces: [],
    }
  },
  created(){
      this.shuffledPieces = _.shuffle(this.pieces);
  },
  methods: {
      clicktile(i){

        if ((i + 1) % 3 === 0){
            console.log("you are at the end of a row")
            this.checkUp(i)
            this.checkDown(i)
            this.checkLeft(i)

        }
        if ((i + 1) % 3 === 1){
            console.log("you are at the beginning of a row")
            this.checkUp(i)
            this.checkDown(i)
            this.checkRight(i)
        }
        if ((i + 1) % 3 === 2){
            console.log("you are at the middle of a row")
            this.checkUp(i)
            this.checkDown(i)
            this.checkLeft(i)
            this.checkRight(i)
        }


      },
      checkUp(index){
        let up = index - 3

        if (up >= 0){
            if (this.shuffledPieces[up] === "empty"){
                console.log("YOU ARE BELOW AN EMPTY PIECE")
                this.swap(up, index)
            }
        }
      },
      checkDown(index){
        let down = index + 3
        if (down <= this.shuffledPieces.length){
            if (this.shuffledPieces[down] === "empty"){
                console.log("YOU ARE ABOVE AN EMPTY PIECE")
                this.swap(down, index)
            }
        }
      },
      checkLeft(index){
        let left = index - 1
        if (left >= 0){
            if (this.shuffledPieces[left] === "empty"){
                console.log("YOU ARE TO THE RIGHT OF AN EMPTY PIECE")
                this.swap(left, index)
            }
        }
      },
    checkRight(index){
        let right = index + 1
        if (right <= this.shuffledPieces.length){
            if (this.shuffledPieces[right] === "empty"){
                console.log("YOU ARE TO THE LEFT OF AN EMPTY PIECE")
                this.swap(right, index)
            }
        }
      },
      swap(empty, index){
        console.log(`swapping ${index} with ${empty}`)
        let tempArr = [ ...this.shuffledPieces]
        var b = tempArr[empty];
        tempArr[empty] = tempArr[index];
        tempArr[index] = b;
        this.shuffledPieces = [ ...tempArr]
        this.validate()
      },
      validate(){
          if (this.pieces.toString() === this.shuffledPieces.toString()){
              alert("YOU WIN!")
          } else {
              console.log("YOU ARE NOT A WINNER")
          }
      }
  }
}
</script>

<style scoped>
    .tile {
        width: 60px;
        height: 60px;
        border: 1px solid black;
        box-sizing: border-box;
        cursor: pointer;
        background-color: white;
    }
    .empty{
        background-color: grey;
        width: 60px;
        height: 60px;
    }

    .tile-container {
        box-sizing: border-box;
        display: flex;
        flex-wrap: wrap;
        width: 182px;
        border: 1px solid black;
        background-color: grey;
    }
    .A {
        background:  url(../assets/A.png);
        background-repeat: no-repeat;
        background-size: 60px 60px;
    }
    .B {
        background:  url(../assets/B.png);
        background-repeat: no-repeat;
        background-size: 60px 60px;
    }
    .C {
        background:  url(../assets/C.png);
        background-repeat: no-repeat;
        background-size: 60px 60px;
    }
    .D {
        background:  url(../assets/D.png);
        background-repeat: no-repeat;
        background-size: 60px 60px;
    }
    .E {
        background:  url(../assets/E.png);
        background-repeat: no-repeat;
        background-size: 60px 60px;
    }
    .F {
        background:  url(../assets/F.png);
        background-repeat: no-repeat;
        background-size: 60px 60px;
    } 
    .G {
        background:  url(../assets/G.png);
        background-repeat: no-repeat;
        background-size: 60px 60px;
    } 
    .H {
        background:  url(../assets/H.png);
        background-repeat: no-repeat;
        background-size: 60px 60px;
    }                  
</style>
