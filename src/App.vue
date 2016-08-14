<template>
    <div class="box">
        <ul class="puzzle-wrap">
            <li
                    :class="{'puzzle':true,'puzzle-empty':!puzzle}"
                    v-for="puzzle in puzzle"
                    v-text="puzzle"
                    @click="moveFn($index)"
            ></li>
        </ul>
        <button class="btn btn-warning btn-block btn-reset" @click="render">重置游戏</button>
    </div>
</template>
<script>
    export default{
        data(){
            return {
                puzzle: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
                puzzles:[]
            }
        },
        ready(){
            this.render();
        },
        methods: {
            //重置渲染
            render(){
                let puzzleArr = [];
                //生成包含1`15数字的数组
                for (let i = 1; i < 16; i++) {
                    puzzleArr.push(i);
                }
                //随机打乱数组 发现打乱数组的方法用排序法打乱,有意思
                puzzleArr = puzzleArr.sort(()=> {
                    return Math.random() - 0.5
                });
                //页面显示
                this.puzzles=puzzleArr;
                this.puzzles.push('');
            },
            //点击方块
            moveFn (index){
                //获取点击位置及其上下左右的值
                let curNum=this.puzzles[index],
                        leftNum=this.puzzles[index-1],
                        rightNum=this.puzzles[index+1],
                        topNum=this.puzzles[index-4],
                        bottomNum=this.puzzles[index+4];
                //和为空的位置交换数值
                if(leftNum ==='' && index!=4 && index!=8 && index!=12){
                    this.puzzles.$set(index-1,curNum);
                    this.puzzles.$set(index,'');
                }else if (rightNum === '' && index!==3 && index!==7 && index!==11){
                    this.puzzles.$set(index+1,curNum);
                    this.puzzles.$set(index,'');
                }else if(topNum===''){
                    this.puzzles.$set(index-4,curNum);
                    this.puzzles.$set(index,'');
                }else if(bottomNum === ''){
                    this.puzzles.$set(index+4,curNum);
                    this.puzzles.$set(index,'');
                }

                this.passFn();
            },
            passFn(){
                if(this.puzzles[15]===''){
                    const newPuzzles=this.puzzles.slice(0,15);
                    const isPass=newPuzzles.every((e,i)=>e===i+1);
                    if(isPass){
                        alert('恭喜,闯关成功!');
                    }
                }
            }
        }
    }
</script>
<style>
    @import url('./assets/css/bootstrap.min.css');
    body {
        font-family: Arial, "Microsoft YaHei";
    }
    .box{
        width:400px;
        margin:50px auto 0;
    }
    .puzzle-wrap{
        width:400px;
        height:400px;
        margin-bottom:40px;
        padding:0;
        background: #ccc;
        list-style: none;
    }
    .puzzle{
        float: left;
        width: 100px;
        height:100px;
        font-size:20px;
        background: #f90;
        text-align: center;
        line-height:100px;
        border:1px solid #cccccc;
        box-shadow:1px 1px 4px;
        text-shadow: 1px 1px 1px #B9B4B4;
        cursor: pointer;
    }
    .puzzle-empty{
        background: #ccc;
        -webkit-box-shadow: inset 2px 2px 18px;
        -moz-box-shadow: inset 2px 2px 18px ;
        box-shadow: inset 2px 2px 18px ;
    }
    .btn-reset{
        -webkit-box-shadow: inset 2px 2px 18px;
        -moz-box-shadow: inset 2px 2px 18px;
        box-shadow: inset 2px 2px 18px;
    }
</style>