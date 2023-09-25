<template>
    <div class="container">
        <div v-if="modal" class="modal">
            <span class="close">
                <img src="../assets/images/icon-close.svg" alt="close" @click="closeModal()">
            </span>
            <div class="modal-content">
                <div class="modal-images">
                    <img v-show="firstImage" class="modal-img" src="../assets/images/image-product-1.jpg"
                        alt="product-image">
                    <img v-show="secondImage" class="modal-img" src="../assets/images/image-product-2.jpg"
                        alt="product-image">
                    <img v-show="thirdImage" class="modal-img" src="../assets/images/image-product-3.jpg"
                        alt="product-image">
                    <img v-show="fourthImage" class="modal-img" src="../assets/images/image-product-4.jpg"
                        alt="product-image">
                </div>
                <div class="modal-thumbnails">
                    <img src="../assets/images/image-product-1-thumbnail.jpg" alt="thumb" class="modal-thumb"
                        @click="showFirstImage()">
                    <img src="../assets/images/image-product-2-thumbnail.jpg" alt="thumb" class="modal-thumb"
                        @click="showSecondImage()">
                    <img src="../assets/images/image-product-3-thumbnail.jpg" alt="thumb" class="modal-thumb"
                        @click="showThirdImage()">
                    <img src="../assets/images/image-product-4-thumbnail.jpg" alt="thumb" class="modal-thumb"
                        @click="showFourthImage()">
                </div>
            </div>
        </div>
        <div class="sidenav" v-if="isSidenav">
            <div class="sidenav-links">
                <img src="../assets/images/icon-close.svg" alt="close" class="sidenav-close" @click="closeNav()">
                <a href="#">Collections</a>
                <a href="#">Men</a>
                <a href="#">Women</a>
                <a href="#">About</a>
                <a href="#">Contact</a>
            </div>
        </div>
        <div class="header">
            <div class="logo-links">
                <img class="sidenav-menu" src="../assets/images/icon-menu.svg" alt="menu" @click="openNav()">
                <img src="../assets/images/logo.svg" alt="sneakers-logo">
                <div class="links">
                    <a href="#">Collections</a>
                    <a href="#">Men</a>
                    <a href="#">Women</a>
                    <a href="#">About</a>
                    <a href="#">Contact</a>
                </div>
            </div>
            <div class="cart-avatar">
                <div class="dropdown">
                    <div class="cart-number">
                        <img @click="openCart()" src="../assets/images/icon-cart.svg" alt="cart">
                        <p v-if="!emptyCart" class="cart-badge">{{ items }}</p>
                    </div>
                    <div v-if="isCart" class="cart" id="cart-dropdown">
                        <p class="cart-title">
                            Cart
                        </p>
                        <hr>
                        <p v-if="emptyCart" class="cart-text">
                            Your cart is empty.
                        </p>
                        <div v-else class="cart-content">
                            <div class="cart-items">
                                <img class="cart-image" src="../assets/images/image-product-1-thumbnail.jpg"
                                    alt="product-image">
                                <div class="cart-content-text">
                                    <p>Fall Limited Edition Sneakers</p>
                                    <p>${{ price }}.00 x {{ items }} <b>${{ cost }}.00</b></p>
                                </div>
                                <img class="cart-delete" src="../assets/images/icon-delete.svg" alt="delete"
                                    @click="clearCart()">
                            </div>
                            <button class="checkout-btn">
                                Checkout
                            </button>
                        </div>
                    </div>
                </div>
                <img src="../assets/images/image-avatar.png" alt="avatar" class="avatar">
            </div>
        </div>
        <div class="product" @click="closeCart(), closeNav()">
            <div class="product-gallery">
                <div class="gallery">
                    <div class="big-image">
                        <img v-show="firstImage" class="main-img" src="../assets/images/image-product-1.jpg"
                            alt="product-image" @click="openModalFirst()">
                        <img v-show="secondImage" class="main-img" src="../assets/images/image-product-2.jpg"
                            alt="product-image" @click="openModalSecond()">
                        <img v-show="thirdImage" class="main-img" src="../assets/images/image-product-3.jpg"
                            alt="product-image" @click="openModalThird()">
                        <img v-show="fourthImage" class="main-img" src="../assets/images/image-product-4.jpg"
                            alt="product-image" @click="openModalFourth()">
                    </div>
                    <div class="thumbnails">
                        <img src="../assets/images/image-product-1-thumbnail.jpg" alt="thumb" class="thumb-img"
                            @click="showFirstImage()">
                        <img src="../assets/images/image-product-2-thumbnail.jpg" alt="thumb" class="thumb-img"
                            @click="showSecondImage()">
                        <img src="../assets/images/image-product-3-thumbnail.jpg" alt="thumb" class="thumb-img"
                            @click="showThirdImage()">
                        <img src="../assets/images/image-product-4-thumbnail.jpg" alt="thumb" class="thumb-img"
                            @click="showFourthImage()">
                    </div>
                </div>
            </div>
            <div class="product-desc">
                <h4 class="comp-name">
                    SNEAKER COMPANY
                </h4>
                <h2 class="prod-name">
                    Fall Limited Edition Sneakers
                </h2>
                <p class="prod-desc">
                    These low-profile sneakers are your perfect casual wear companion. Featuring a durable rubber outer
                    sole,
                    they'll withstand everything the weather can offer.
                </p>
                <div class="prices">
                    <h3 class="price">
                        ${{ price }}.00 <span class="discount">50%</span>
                    </h3>
                    <h5 class="old-price">$250.00</h5>
                </div>
                <div class="add-to-cart">
                    <div class="counter">
                        <button class="counter-btn" @click="subCount()">-</button>
                        <span class="count">{{ count }}</span>
                        <button class="counter-btn" @click="addCount()">+</button>
                    </div>
                    <button class="cart-btn" @click="addToCheckout()">
                        <img src="../assets/images/icon-cart.svg" alt="cart">
                        Add to cart
                    </button>
                </div>
            </div>
        </div>
        <div class="attribution">
            Challenge by <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>.
            Coded by <a href="https://twitter.com/DarkerArcher" target="_blank">Ayo Otutuloro</a>.
        </div>
    </div>
</template>

<script>
export default {
    name: 'SneakersProduct',
    data() {
        return {
            count: 0,
            price: 125,
            cost: 0,
            items: 0,
            firstImage: true,
            secondImage: false,
            thirdImage: false,
            fourthImage: false,
            modal: false,
            cart: document.getElementById("cart-dropdown"),
            isCart: false,
            emptyCart: true,
            isSidenav: false,
        }
    },
    methods: {
        addCount() {
            this.count++
        },
        subCount() {
            if (this.count === 0) {
                this.count = 0
            } else {
                this.count--
            }
        },
        showFirstImage() {
            this.firstImage = true;
            this.secondImage = false;
            this.thirdImage = false;
            this.fourthImage = false;
        },
        showSecondImage() {
            this.firstImage = false;
            this.secondImage = true;
            this.thirdImage = false;
            this.fourthImage = false;
        },
        showThirdImage() {
            this.firstImage = false;
            this.secondImage = false;
            this.thirdImage = true;
            this.fourthImage = false;
        },
        showFourthImage() {
            this.firstImage = false;
            this.secondImage = false;
            this.thirdImage = false;
            this.fourthImage = true;
        },
        openModalFirst() {
            this.modal = true;
            this.firstImage = true;
            this.secondImage = false;
            this.thirdImage = false;
            this.fourthImage = false;
        },
        openModalSecond() {
            this.modal = true;
            this.firstImage = false;
            this.secondImage = true;
            this.thirdImage = false;
            this.fourthImage = false;
        },
        openModalThird() {
            this.modal = true;
            this.firstImage = false;
            this.secondImage = false;
            this.thirdImage = true;
            this.fourthImage = false;
        },
        openModalFourth() {
            this.modal = true;
            this.firstImage = false;
            this.secondImage = false;
            this.thirdImage = false;
            this.fourthImage = true;
        },
        closeModal() {
            this.modal = false
        },
        openCart() {
            this.isCart = !this.isCart
        },
        addToCheckout() {
            if (this.count != 0) {
                this.items = this.count;
                this.cost = this.items * this.price;
                this.emptyCart = false;
                this.count = 0;
            }
        },
        clearCart() {
            this.items = 0;
            this.cost = 0;
            this.emptyCart = true;
        },
        closeCart() {
            this.isCart = false;
        },
        openNav() {
            this.isSidenav = true;
        },
        closeNav() {
            this.isSidenav = false
        }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Kumbh+Sans:wght@400;700&display=swap');

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Kumbh Sans', sans-serif;
}

.dropdown {
    float: left;
    overflow: hidden;
}

.cart {
    position: absolute;
    right: 100px;
    top: 145px;
    background-color: #f9f9f9;
    min-width: 350px;
    min-height: 200px;
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
    z-index: 1;
    border-radius: 15px;
}

.cart-badge {
    color: rgb(0, 0, 0);
    font-weight: 700;
    border-radius: 50%;
    width: 25px;
    height: 25px;
    padding: 0;
}

.cart-number {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: baseline;
}

.cart-title {
    text-align: left;
    padding: 20px 0 20px 10px;
    font-weight: 700;
    color: rgb(0, 0, 0);
}

.cart-text {
    text-align: center;
    padding: 50px 0;
    font-weight: 700;
    color: rgb(104, 112, 125);
}

.container {
    margin: 0 100px 0;
}

.header {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    border-bottom: solid 1px rgba(104, 112, 125, 0.5);
}

.logo-links {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    gap: 100px;
}

.links {
    display: flex;
    flex-direction: row;
    justify-content: space-around;
    gap: 20px;
}

.links a {
    text-decoration: none;
    color: rgb(104, 112, 125);
    padding: 30px 0;
}

.links a:hover {
    border-bottom: 1px solid rgb(255, 125, 26);
    cursor: pointer;
}

.cart-avatar {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    gap: 20px;
}

.cart-avatar img:hover {
    cursor: pointer;
}

.avatar {
    width: 50px;
}

.avatar:hover {
    border: 2px solid rgb(255, 125, 26);
    border-radius: 50%;
}

.product {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 20px;
    padding: 30px 0 0 0;
}

.product-gallery {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: 50%;
}

.product-desc {
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: left;
    gap: 5px;
    width: 50%;
}

.comp-name {
    font-size: 15px;
    color: rgb(255, 125, 26);
}

.prod-name {
    font-size: 60px;
    color: rgb(0, 0, 0);
}

.prod-desc {
    font-size: 20px;
    color: rgb(104, 112, 125);
}

.prices {
    display: flex;
    flex-direction: column;
}

.price {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 5px;
    color: rgb(0, 0, 0);
    font-size: 30px;
}

.old-price {
    text-decoration: line-through;
    color: rgb(104, 112, 125);
}

.discount {
    font-size: 10px;
    padding: 5px;
    border-radius: 5px;
    color: rgb(255, 125, 26);
    background-color: rgb(255, 237, 224);
}

.add-to-cart {
    display: flex;
    flex-direction: row;
    gap: 10px;
}

.counter {
    display: flex;
    flex-direction: row;
    align-items: center;
    border-radius: 5px;
    padding: 5px 15px;
    background-color: rgb(247, 248, 253);
}

.count {
    padding: 0 15px;
    font-weight: 700;
}

.counter-btn {
    text-align: center;
    color: rgb(255, 125, 26);
    font-weight: 700;

    padding: 5px 15px;
    background-color: rgb(247, 248, 253);
    border: none;

    cursor: pointer;
}

.cart-btn {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 5px;
    border: none;
    background-color: rgb(255, 125, 26);
    color: rgb(255, 255, 255);
    padding: 10px 50px;
    border-radius: 5px;
    cursor: pointer;
    font-weight: 700;
}

.cart-btn:hover {
    background-color: rgb(238, 169, 119);
}

.gallery {
    display: flex;
    flex-direction: column;
    width: 300px;
    gap: 10px;
}

.main-img {
    width: 400px;
    border-radius: 20px;
}

.main-img:hover {
    cursor: pointer;
}

.thumbnails {
    display: flex;
    flex-direction: row;
    gap: 10px;
}

.thumb-img {
    width: 93px;
    cursor: pointer;
    opacity: 1;
    border-radius: 12px;
}

.thumb-img:hover {
    opacity: 0.6;
}

.main-images {
    display: none;
}

.modal {
    display: flex;
    flex-direction: column;
    align-items: center;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(0, 0, 0, 0.75);
}

.modal-content {
    position: relative;
    margin: auto;
    padding: 0;
    width: 90%;
    max-width: 1200px;
    display: flex;
    flex-direction: column;
    gap: 25px;

}

.modal-img {
    width: 600px;
    border-radius: 30px;
}

.modal-thumbnails {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 10px;
}

.modal-thumb {
    width: 100px;
    border-radius: 15px;
}

.modal-thumb:hover {
    cursor: pointer;
    opacity: 0.6;
}

.close {
    position: absolute;
    top: 90px;
    right: 35%;
}

.close:hover {
    cursor: pointer;
}

.cart-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 15px;
    padding: 30px 0;
}

.cart-items {
    display: flex;
    flex-direction: row;
    align-items: center;
    gap: 10px;
}

.cart-image {
    width: 50px;
    border-radius: 5px;
}

.cart-content-text {
    display: flex;
    flex-direction: column;
    color: rgb(104, 112, 125);
    text-align: left;
}

.cart-content-text b {
    color: rgb(0, 0, 0);
}

.checkout-btn {
    border: none;
    background-color: rgb(255, 125, 26);
    color: rgb(255, 255, 255);
    padding: 20px 50px;
    border-radius: 5px;
    cursor: pointer;
    font-weight: 700;
    width: 84%;
}

.sidenav-menu {
    display: none;
}

.sidenav {
    height: 100%;
    width: 250px;
    position: fixed;
    z-index: 1;
    top: 0;
    left: 0;
    background-color: rgb(255, 255, 255);
    overflow-x: hidden;
    transition: 0.5s;
    padding-top: 60px;
}

.sidenav a {
    padding: 8px 8px 8px 32px;
    text-decoration: none;
    text-align: left;
    font-size: 25px;
    font-weight: 700;
    color: rgb(0, 0, 0);
    display: block;
    transition: 0.3s;
}

.sidenav .sidenav-close {
    position: absolute;
    top: 25px;
    left: 25px;
    color: black;
}

@media (max-width: 1200px) {
    .container {
        margin: 0 50px 0;
    }

    .logo-links {
        gap: 50px;
    }

    .product {
        gap: 50px;
    }
}

@media (max-width: 768px) {
    .main-img {
        width: 100%;
    }

    .thumbnails {
        width: 100%;
    }

    .thumb-img {
        width: 25%;
    }

    .prod-name {
        font-size: 40px;
    }

    .prod-desc {
        font-size: 16px;
    }

    .price {
        font-size: 25px;
    }
}

@media (max-width: 600px) {
    .container {
        margin: 0 20px 0;
    }

    .header {
        width: 100%;
        padding-bottom: 10px;
    }

    .logo-links {
        gap: 20px;
    }

    .links {
        display: none;
    }

    .sidenav-menu {
        display: flex;
        flex-direction: row;
    }

    .cart-avatar {
        gap: 5px;
    }

    .product {
        flex-direction: column;
        align-items: center;
    }

    .product-gallery {
        width: 95%;
    }

    .thumb-img {
        width: 23%;
    }

    .product-desc {
        width: 95%;
    }

    .cart {
        right: 0;
        min-width: 100%;
    }

    .add-to-cart {
        flex-direction: column;
    }

    .counter {
        font-size: 30px;
        padding: 20px 0;
    }

    .counter-btn {
        font-size: 30px;
        width: 100%;
    }

    .cart-btn {
        justify-content: center;
        padding: 20px 10px;
        font-size: 20px;
    }

    .modal {
        display: none;
    }
}

.attribution {
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translate(-50%);
    padding: 15px 0;
    font-size: 11px;
    text-align: center;
}

.attribution a {
    color: hsl(228, 45%, 44%);
}</style>