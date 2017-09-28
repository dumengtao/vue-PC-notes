<template>
    <div class="list">
    	<div class="list-header">
    		<div class="title">NOTES | COLIGO</div>
    		<div class="nav">
    			<button class="all" :class="{ changeCol: allCol }" @click="allShow()">All Notes</button>
    			<button class="fav" :class="{ changeCol: favCol }" @click="favShow()">Favorites</button>
    		</div>
    	</div>
    	<div class="list-content">
    		<div class="allNotes" v-if="allCol">
    			<div class="title" :class="{ active: nowIndex === index }" @click="activeNote(index)" v-for="(item,index) in items">{{ item.value }}</div>
    		</div>
    		<div class="favNotes" v-else>
                <div class="title">收藏功能还在酝酿中...</div>
            </div>
    	</div>
    </div>
</template>

<script type="ecmascript-6">
	import bus from '../common/js/bus.js'

    export default {
    	data() {
    		return {
    			allCol: true,
    			favCol: false,
                nowIndex: 0,
                items: []
    		}
    	},
    	created() {
            // H5本地获取数据
            let data = JSON.parse(localStorage.getItem('listData'))
            for(let i in data){
                this.items.push(data[i])
            }
            
    		bus.$on('addNote',() => {
    			const t = { value: "New Note" }
    			this.items.push(t)
    		})
    		bus.$on('favNote',() => {
                this.$message('收藏功能还未上线，请等候通知!')
    		})
    		bus.$on('deleteNote',() => {
                this.items.splice(this.nowIndex,1)
                if(this.nowIndex > 0){
                    this.nowIndex--
                }else{
                    this.nowIndex = 0
                }
    		})
            bus.$on('titleChange',(msg,index) => {
                this.items.splice(index,1,{ value: msg })
            })
    	},
    	methods: {
    		allShow() {
    			this.allCol = true
    			this.favCol = false
    		},
    		favShow() {
    			this.allCol = false
    			this.favCol = true
    		},
    		activeNote(index) {
    			this.nowIndex = index
                bus.$emit('showContent',this.nowIndex)
    		}
    	},
        beforeUpdate() {
            // H5本地储存数据
            localStorage.setItem('listData',JSON.stringify(this.items))
        }
    }
</script>

<style lang="stylus" rel="stylesheet/stylus">
    .list
        box-sizing border-box
        background-color #f5f5f5
        font-family 'Raleway', sans-serif
        .list-header
            padding 5px 25px 25px 25px
            font-weight 400
            font-family inherit
            .title
                padding-bottom 8px
                margin 20px 0 10px
                font-size 22px
                color #666
                font-weight 300
                line-height 1.1
                font-family inherit
            .nav
                display inline-flex
                width 100%;
                height: 34px
                .all,.fav
                    width 125px
                    height 34px
                    line-height 34px
                    background-color #fff
                    color #666
                    font-size 14px
                    border 1px solid #adadad
                    padding 0
                    cursor pointer
                .all
                    border-top-left-radius 4px
                    border-bottom-left-radius 4px
                    &.changeCol
                        background-color #e6e6e6
                        box-shadow inset 0 3px 5px rgba(0,0,0,.125)
                .fav
                    border-top-right-radius 4px
                    border-bottom-right-radius 4px
                    &.changeCol
                        background-color #e6e6e6
                        box-shadow inset 0 3px 5px rgba(0,0,0,.125)
    .list-content
        height 100%
        .allNotes,.favNotes
            height 100%
            .title
                display inline-block         
                box-sizing border-box
                width 100%
                height 40px
                padding 10px 0     
                color #555
                white-space nowrap            
                background-color #fff
                border-bottom 1px solid #f5f5f5
                cursor pointer
                &.active
                    color #fff
                    background-color #337ab7
</style>
