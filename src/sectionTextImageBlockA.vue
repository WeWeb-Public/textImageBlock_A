<template>
    <div class="textimageblock_A">
        <!-- wwManager:start -->
        <wwSectionEditMenu v-bind:sectionCtrl="sectionCtrl"></wwSectionEditMenu>
        <!-- wwManager:end -->

        <wwObject v-bind:ww-object="section.data.background" class="background" ww-category="background"></wwObject>

        <div class="container section-padding">
            <div class="row">
                <div class="titles">
                    <h1 class="section-title"><wwObject v-bind:ww-object="section.data.title"></wwObject></h1>
                    <h2 class="section-subtitle"><wwObject v-bind:ww-object="section.data.subtitle"></wwObject></h2>
                </div>
            </div>

            <div class="row margint20">
                
                <div class="blocks" v-for="(block, index) in section.data.blocks" :key="block.uniqueId" :class="{'left': !(index % 2)}">
                    <wwObject class="block-img-container" v-bind:ww-object="block.img"></wwObject>
                    <wwObject class="block-title" v-bind:ww-object="block.title"></wwObject>
                    <wwObject class="block-text" v-bind:ww-object="block.text"></wwObject>
                    <wwObject class="block-text" v-bind:ww-object="block.text2"></wwObject>
                    <div class="button-container">
                        <wwObject class="button-wrapper" v-bind:ww-object="block.button"></wwObject>
                    </div>
            
                    <!-- wwManager:start -->
                    <div class="edit-button-top-left" @click="removeBlock(index)">
                        <i class="wwi wwi-delete" aria-hidden="true"></i>
                    </div>
                    <!-- wwManager:end -->
                </div>

                <!-- wwManager:start -->
                <div class="blocks add-block" :class="{'left': section.data.blocks && !(section.data.blocks.length % 2)}">
                    <div class="plus" @click="addBlock()">
                        <i class="wwi wwi-add" aria-hidden="true"></i>
                    </div>
                </div>
                <!-- wwManager:end -->

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "TextAndImageBlock_A",
    props: {
        sectionCtrl: Object
    },
    data() {
        return {}
    },
    computed: {
        section() {
            return this.sectionCtrl.get();
        }
    },
    created() {
        this.initData()
    },
    methods: {
        getNewBlock() {
            const data = {}

            data.img = wwLib.wwObject.getDefault({ type: 'ww-image' });
            data.text = wwLib.wwObject.getDefault({ type: 'ww-text', data: { text: 'Start editing by hitting the pen!' } });
            data.text2 = wwLib.wwObject.getDefault({ type: 'ww-text' });
            data.title = wwLib.wwObject.getDefault({ type: 'ww-text', data: { text: 'Use it to illustrate your story, products or services...' } });
            data.button = wwLib.wwObject.getDefault({ type: 'ww-button', data: { color: 'black', borderColor: 'black' } });
    
            return data;
        },
        initData() {
            this.section.data = this.section.data || {};
    
            if (_.isEmpty(this.section.data.blocks))
                this.section.data.blocks = [this.getNewBlock(), this.getNewBlock()];
            
            if (!this.section.data.background)
                this.section.data.background = wwLib.wwObject.getDefault({ type: 'ww-color' });

            if (!this.section.data.title)
                this.section.data.title = wwLib.wwObject.getDefault({ type: 'ww-text' });
            
            if (!this.section.data.subtitle)
                this.section.data.subtitle = wwLib.wwObject.getDefault({ type: 'ww-text' });

            this.sectionCtrl.update(this.section);
        },
        addBlock(options) {
            this.section.data.blocks.push(this.getNewBlock());
            this.sectionCtrl.update(this.section);
        },
        removeBlock(index) {
            this.section.data.blocks.splice(index, 1);
            this.sectionCtrl.update(this.section);
        }
    }
};
</script>

<style scoped>
.textimageblock_A .container {
    width: 100%;
    position: relative;
}

.textimageblock_A .background {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
}

.textimageblock_A .block-img-container {
    width: 100%;
    position: relative;
}

.textimageblock_A .block-title {
    margin-top: 10px;
}

.textimageblock_A .block-text {
    margin-top: 10px;
}

.textimageblock_A .button-container {
    text-align: center;
    width: 100%;
    margin-top: 20px;
    margin-bottom: 40px;
}

.textimageblock_A .section-subtitle {
    margin-top: 10px;
}

.textimageblock_A .section-padding {
    padding: 30px 15px
}

.textimageblock_A .margint20 {
    margin-top: 20px;
}

.textimageblock_A .row {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -15px;
    margin-left: -15px;
}

.textimageblock_A .plus {
  color: white;
  cursor: pointer;
  pointer-events: all;
  font-size: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;
  height: 40px;
  border-radius: 100%;
  background-color: #1763A9;
  background: linear-gradient(to right, #1763A9 0%, #2E85C2 100%);
}

.textimageblock_A .add-block {
    display: flex;
    justify-content: center;
}

.textimageblock_A .edit-button-top-left {
    position: absolute;
    left: -2px;
    top: -17px;
    width: 36px;
    height: 36px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 100%;
    text-align: center;
    font-size: 18px;
    line-height: 36px;
    cursor: pointer;
    pointer-events: all;
    z-index: 3;
    color: white;
    background-color: #E73055;
    background: linear-gradient(to right, #E73055 0%, rgb(175, 33, 61) 100%);
}

.textimageblock_A .titles {
    position: relative;
    width: 100%;
    min-height: 1px;
    padding-right: 15px;
    padding-left: 15px;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
}

.textimageblock_A .blocks {
    position: relative;
    width: 100%;
    min-height: 1px;
    padding-right: 15px;
    padding-left: 15px;
    -ms-flex: 0 0 100%;
    flex: 0 0 100%;
    max-width: 100%;
    margin-bottom: 20px;
}

@media (min-width: 768px) {
    .textimageblock_A .button-container {
        margin-bottom: 20px;
    }
    .textimageblock_A .section-padding {
        padding: 50px 30px
    }
    .textimageblock_A .blocks {
        -ms-flex: 0 0 50%;
        flex: 0 0 50%;
        max-width: 50%;
    }
}

@media (min-width: 992px) {
    .textimageblock_A .section-padding {
        padding: 75px 50px
    }
    .textimageblock_A .blocks {
        -ms-flex: 0 0 41.666666%;
        flex: 0 0 41.666666%;
        max-width: 41.666666%;
    }
    .textimageblock_A .blocks.left {
        margin-left: 8.333333%;
    }
}

@media (min-width: 1024px) {
    .textimageblock_A .blocks {
        -ms-flex: 0 0 33.333333%;
        flex: 0 0 33.333333%;
        max-width: 33.333333%;
    }
    .textimageblock_A .blocks.left {
        margin-left: 16.666666%;
    }
}

@media (min-width: 1200px) {}
</style>
