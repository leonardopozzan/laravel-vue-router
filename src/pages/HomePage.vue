<template>
    <div class="home-page pt-5">
        <h1 class="text-center">Who am I?</h1>
        <p class="pt-3 pb-5">Lorem ipsum dolor sit amet, consectetur adipisicing elit. Saepe libero modi natus soluta incidunt nostrum nihil sint quam, similique sed consequuntur provident, esse autem vel suscipit officiis magni eius dicta dolorum. Vitae error neque aliquid, iusto labore corporis perferendis reiciendis impedit cupiditate unde optio maxime qui debitis quibusdam, saepe sequi recusandae odit animi tempora. Aut illo inventore amet, odio laudantium porro, quo voluptatem quam perspiciatis rem magnam! Doloribus quibusdam dignissimos impedit veritatis. Explicabo vel praesentium impedit? Architecto magni sequi quia ab sapiente ut? Odit quas eligendi, fuga nam vero est ea saepe repellendus quo, quaerat atque nostrum deserunt, omnis sed!</p>
        <div class="inner-home row">
            <div class="col-12 my-card">
                <div class="inner-card">
                    <div class="img-box">
                        <img src="https://avatars.githubusercontent.com/u/108693204?v=4" alt="">
                    </div>
                    <div class="description py-3">I am happy to know you that 300+ project done successfully</div>
                    <router-link :to="{name : 'projects'}"><button>See More</button></router-link>
                </div>
            </div>
        </div>  
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>
@use '../assets/style/mixines' as *;
@use '../assets/style/variables' as *;
.home-page{
    h1{
    font-family: 'Bowlby One SC', cursive;
    font-size: 60px;
    }
    p{
        text-align: center;
    }
    .my-card{
        background-color: $light-blue;
        .inner-card{
            padding: 2.5rem 1.5rem;
            color: white;
            text-align: center;
            .img-box{
                margin: auto;
                width: 300px;
                height: 300px;
                border-radius: 50%;
                overflow: hidden;
            }
            .description{
                font-size: 2rem;
            }
            button{
                background-color: $light-blue;
                padding: 0.8rem 3.5rem ;
                border: 3px solid white;
                color: white;
            }
        }
    }
}

</style>