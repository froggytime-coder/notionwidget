<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Image Carousel</title>

<style>
body {
    margin: 0;
    padding: 20px;
    font-family: Arial, sans-serif;
    background: transparent;
}

.carousel {
    position: relative;
    width: 100%;
    max-width: 1000px;
    aspect-ratio: 4 / 3;
    overflow: hidden;
    margin: auto;
}

.slides {
    display: flex;
    transition: transform 0.5s ease;
    align-items: center;
}

.slide {
    flex: 0 0 auto;
    width: 80%;
    box-sizing: border-box;
    padding: 0 10px;
}

.slide.active {
    opacity: 1;
    transform: scale(1);
}

.slide img {
    width: 100%;
    height: 100%;
    object-fit: contain;
    border-radius: 12px;
    display: block;
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

button:hover {
    background: rgba(0,0,0,0.7);
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
    transition: background 0.3s ease;
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
            <img src="curiousgeorge.jpg" alt="Photo 1">
        </div>

        <div class="slide">
            <img src="image (1).png" alt="Photo 2">
        </div>

        <div class="slide">
            <img src="image (3).png" alt="Photo 3">
        </div>
        
        <div class="slide">
            <img src="bhagavad-gita-wallpapers-libro_grande.jpg" alt="Photo 4">
        </div>

        <div class="slide">
            <img src="thumbnail_IMG_5388.jpg" alt="Photo 5">
        </div>

    </div>

    <button class="prev" onclick="changeSlide(-1)">❮</button>
    <button class="next" onclick="changeSlide(1)">❯</button>

    <div class="dots" id="dots"></div>

</div>

<script>
const slidesContainer = document.getElementById('slides');
const slideElements = document.querySelectorAll('.slide');
const dotsContainer = document.getElementById('dots');

const totalSlides = slideElements.length;
let currentSlide = 0;

// Create dots
for (let i = 0; i < totalSlides; i++) {
    const dot = document.createElement('span');
    dot.classList.add('dot');
    dot.addEventListener('click', () => {
        currentSlide = i;
        updateCarousel();
    });
    dotsContainer.appendChild(dot);
}

function updateCarousel() {

   const slideWidth = slideElements[0].offsetWidth;

slidesContainer.style.transform =
    `translateX(-${currentSlide * slideWidth}px)`;

    slideElements.forEach((slide, index) => {
        slide.classList.toggle('active', index === currentSlide);
    });

    document.querySelectorAll('.dot').forEach((dot, index) => {
        dot.classList.toggle('active', index === currentSlide);
    });
}

function changeSlide(direction) {
    currentSlide =
        (currentSlide + direction + totalSlides) % totalSlides;
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
