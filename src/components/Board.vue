<template>
    <div id="board" :style = "boardStyle">
        
        <square
        v-for = "block in squares"
        :id = "block.id"
        :key = "block.id"
        :style = "block.squareStyle">
        </square>
        
    </div>
</template>

<script>
import square from "./square";

           
        const boardWidth = 8;
        const boardHeight = 8;
        const boardArea = boardWidth * boardHeight;
        const squareSize = 50;

export default {
    name: "Board",
    components: {
        square,
    },
    data() {
        return {
            squares: [],
            row: 0,
            columnArray: ['a','b', 'c', 'd','e','f', 'g', 'h'],
            boardStyle: {
                display: "grid",
                gridTemplateRows: `repeat(${boardHeight}, ${squareSize}px)`,
                gridTemplateColumns: `repeat(${boardWidth}, ${squareSize}px)`
            }
        }
    },
    methods: {
        
        makeIds(index) {
            console.log("makeIds")
            //get letter from array and repeat for each row
            let column = this.columnArray[index % boardWidth];
            //increment row every time a new row starts
            if (index % boardWidth === 0){
                this.row += 1;
            }
            
            return `square-${column}${this.row}` 
        },
        makeSquareStyle() {
            
        },
        alternateColor() {

        },
        repeatSquare() {
            console.log('repeatSquare');
            for (let i = 0; i < boardArea; i++) {
                this.squares.push(               
                    {
                        id: this.makeIds(i),
                        squareStyle:{
                        width: "50px",
                        height: "50px",
                        backgroundColor: "#000",    
                        }

                });  
            }   
        }
    },
    created(){
        
       this.repeatSquare(boardArea);


    }


}
</script>