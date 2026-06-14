<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Image Carousel</title>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: transparent;
}

.carousel {
    position: relative;
    width: 100%;
    max-width: 800px;
    aspect-ratio: 16 / 9;
    overflow: hidden;
    border-radius: 12px;
}

.slides {
    display: flex;
    transition: transform 0.5s ease-in-out;
    height: 100%;
}

.slide {
    min-width: 100%;
    height: 100%;
}

.slide img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

button {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    border: none;
    background: rgba(0,0,0,0.5);
    color: white;
    font-size: 24px;
    padding: 12px;
    cursor: pointer;
    border-radius: 50%;
    z-index: 10;
}

.prev {
    left: 10px;
}

.next {
    right: 10px;
}

.dots {
    position: absolute;
    bottom: 15px;
    width: 100%;
    text-align: center;
}

.dot {
    display: inline-block;
    width: 10px;
    height: 10px;
    margin: 0 4px;
    border-radius: 50%;
    background: rgba(255,255,255,0.5);
    cursor: pointer;
}

.dot.active {
    background: white;
}
</style>
</head>

<body>

<div class="carousel">
    <div class="slides" id="slides">
        <div class="slide">
            <img src="https://drive.google.com/uc?export=download&id=1OtWUx-BdsYK8ApEIUzvBM2itsh6z2giP" alt="">
        </div>
        <div class="slide">
            <img src="https://drive.google.com/uc?export=download&id=126jNEgjbycX65jTXRdZ6JIEecWrxKlGG" alt="">
        </div>
        <div class="slide">
            <img src="https://drive.google.com/uc?export=download&id=1_-QO7-60GyhGpLVjDednjnRxD7_xxm4G" alt="">
        </div>
    </div>

    <button class="prev" onclick="changeSlide(-1)">❮</button>
    <button class="next" onclick="changeSlide(1)">❯</button>

    <div class="dots" id="dots"></div>
</div>

<script>
const slides = document.getElementById('slides');
const totalSlides = document.querySelectorAll('.slide').length;
const dotsContainer = document.getElementById('dots');

let currentSlide = 0;

for (let i = 0; i < totalSlides; i++) {
    const dot = document.createElement('span');
    dot.classList.add('dot');
    dot.addEventListener('click', () => goToSlide(i));
    dotsContainer.appendChild(dot);
}

function updateCarousel() {
    slides.style.transform = `translateX(-${currentSlide * 100}%)`;

    document.querySelectorAll('.dot').forEach((dot, index) => {
        dot.classList.toggle('active', index === currentSlide);
    });
}

function changeSlide(direction) {
    currentSlide = (currentSlide + direction + totalSlides) % totalSlides;
    updateCarousel();
}

function goToSlide(index) {
    currentSlide = index;
    updateCarousel();
}

// Auto-advance every 5 seconds
setInterval(() => {
    currentSlide = (currentSlide + 1) % totalSlides;
    updateCarousel();
}, 5000);

updateCarousel();
</script>

</body>
</html>
