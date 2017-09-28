<template>
    <div class="select">
    	<div class="add" @click="addNote()"><i class="icon-plus"></i></div>
    	<div class="collect" @click="favNote()"><i class="icon-star-full"></i></div>
    	<div class="delete" @click="deleteNote()"><i class="icon-cross"></i></div>
    </div>
</template>

<script type="ecmascript-6">
	import bus from '../common/js/bus.js'

    export default {
    	methods: {
    		addNote() {
                this.$message({
                    message: '恭喜您，成功添加新笔记!',
                    type: 'success'
                })
    			bus.$emit('addNote')
    		},
    		favNote() {
    			bus.$emit('favNote')
    		},
    		deleteNote() {
                this.$confirm('是否删除该笔记!', '温馨提醒', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning',
                    closeOnClickModal: false
                }).then(() => {
                    bus.$emit('deleteNote')
                    this.$message({
                        type: 'success',
                        message: '删除成功!'
                    })
                }).catch(() => {
                    this.$message({
                        type: 'info',
                        message: '已取消删除!'
                    })
                })
    		}
    	}
    }
</script>

<style lang="stylus" rel="stylesheet/stylus">
    .select
        box-sizing border-box
        background-color #30414d
        color #767676
        padding 35px 25px 25px 25px
        .add,.collect,.delete
            margin-bottom 35px
            width 30px
            height 36px
            cursor pointer
            .icon-plus,.icon-cross
                opacity .8
                font-size 25px
                line-height 36px
            .icon-star-full
                opacity .8
                font-size 30px
                line-height 36px
                &.fav
                    color #F7AE4F
</style>
