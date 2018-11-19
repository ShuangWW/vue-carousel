<template>
    <div class="carousel-wrap" id="carousel">
        <transition-group tag="ul" class='slide-ul' name="list">
            <li v-for="(img,index) in slideList" :key="index" v-show="index===currentIndex" @mouseenter="stop" @mouseleave="go">
                <img :src="img">
            </li>
        </transition-group>
        <div class="carousel-items">
            <span v-for="(item,index) in slideList.length" :key="index" :class="{'active':index===currentIndex}" @mouseover="change(index)"></span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Swiper',
    data() {
        return {
            slideList: [
                require('../assets/img/1.jpg'),
                require('../assets/img/2.jpg'),
                require('../assets/img/3.jpg'),
                require('../assets/img/4.jpg'),
                require('../assets/img/5.jpg')
            ],
            currentIndex: 0,
            timer: ''
        }
    },
    methods: {
        go() {
            this.timer = setInterval(() => {
                this.autoPlay()
            }, 4000)
        },
        stop() {
            clearInterval(this.timer)
            this.timer = null
        },
        change(index) {
            this.currentIndex = index
        },
        autoPlay() {
            this.currentIndex++;
            if (this.currentIndex > this.slideList.length - 1) {
                this.currentIndex = 0
            }
        }
    },
    created() {
        this.$nextTick(() => {
            this.timer = setInterval(() => {
                this.autoPlay()
            }, 4000)
        })
    }
}
</script>

<style lang="scss" scoped>
.carousel-wrap {
	height: 300px;
	width: 533px;
	overflow: hidden;
	background-color: #fff;
	margin: 0 auto;
	position: relative;
	.slide-ul {
		position: relative;
		width: 100%;
		height: 100%;
		margin: 0px;
		padding: 0px;
		li {
			position: absolute;
			width: 100%;
			height: 100%;
			img {
				width: 100%;
				height: 100%;
			}
		}
		.list-enter-to {
			transition: all 1s ease;
			transform: translateX(0);
		}

		.list-leave-active {
			transition: all 1s ease;
			transform: translateX(-100%);
		}

		.list-enter {
			transform: translateX(100%);
		}

		.list-leave {
			transform: translateX(0);
		}
	}
	.carousel-items {
		position: absolute;
		z-index: 10;
		bottom: 20px;
		width: 100%;
		text-align: center;
		span {
			display: inline-block;
			height: 6px;
			width: 30px;
			margin: 0 3px;
			background-color: #b2b2b2;
			cursor: pointer;
		}
		.active {
			background-color: orange;
		}
	}
}
</style>

