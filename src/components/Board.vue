<template>
    <div id="board" >
        
        <selector />
        
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
import selector from "./selector";

           
        const boardWidth = 8;
        const boardHeight = 8;
        const boardArea = boardWidth * boardHeight;
        const squareSide = 50;
        let row = 0;
        let coordinates = {};

export default {
    name: "Board",
    components: {
        square,
        selector,
    },
    data() {
        return {
            squares: [],
            columnArray: ['a','b', 'c','d','e','f', 'g', 'h'],
            selectorLocation: "square-a1",
        }
    },
    methods: {
        
        makeIds(index) {
            
           
            //get letter from array and repeat for each row
            let column = this.columnArray[index % boardWidth];
            //increment row every time a new row starts
            if (index % boardWidth === 0){
                row += 1;
            }
            
            let id = `square-${column}${row}`;
            this.makeSquareCoordinates(column, row);
            this.makeSelector(id);
            return id; 
        },
        makeSquareStyle() {
            
        },
        alternateColor(color1, color2, index) {
         let color = "";
         //alternate between two colors
              
            if(index % 2 === 0){
                    color = color1;
                };
            if(index % 2 === 1){
                    color = color2;
                };
           
         //reverse alternation every row if boardWidth is even
            
            if(boardWidth % 2 === 0){
                if(index % (boardWidth * 2) >= boardWidth)
                    if(color === color1){
                        color = color2;
                    }else if(color === color2){
                        color = color1
                    }    
            }
            return color;
            
         },
        makeSquareCoordinates(column,row) {
            coordinates.marginLeft= squareSide * (this.columnArray.indexOf(column) + 1);
            coordinates.marginTop = squareSide * row;
        },
        makeSelector(id){
            
            let selector = false;

            if (id === this.selectorLocation) {
                selector = true;
            };
            
            return selector;
        },
        repeatSquare(color) {
           
            for (let i = 0; i < boardArea; i++) {
                this.squares.push(               
                    {
                        id: this.makeIds(i),
                        selector: this.makeSelector(),
                        squareStyle:{
                        position: "absolute",
                        width: `${squareSide}px`,
                        height: `${squareSide}px`,
                        backgroundColor: this.alternateColor('#2003fc','#05021a',i), 
                        marginLeft: `${coordinates.marginLeft}px`,
                        marginTop: `${coordinates.marginTop}px`,   
                    }
                });  
               
            }   
        }
    },
    created(){
        
       this.repeatSquare(boardArea);
    
    },


}
</script>