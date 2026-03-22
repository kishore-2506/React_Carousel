# Ex05 Image Carousel
## Date:19.03.26

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM

# App.jsx
```
import React from "react";
import Carousel from "./Carousel";
import "./index.css";

function App() {
  return (
    <div className="app">
      <h2 className="title">Image Carousel</h2>
      <Carousel />
    </div>
  );
}

export default App;
```
# Carousel.jsx
```
import React, { useState, useEffect } from "react";
import "./Carousel.css";

const images = [
  "https://picsum.photos/id/1018/600/400",
  "https://picsum.photos/id/1015/600/400",
  "https://picsum.photos/id/1019/600/400"
];

function Carousel() {
  const [currentIndex, setCurrentIndex] = useState(0);

  const nextImage = () => {
    setCurrentIndex((currentIndex + 1) % images.length);
  };

  const prevImage = () => {
    setCurrentIndex(
      (currentIndex - 1 + images.length) % images.length
    );
  };

  useEffect(() => {
    const interval = setInterval(nextImage, 3000);
    return () => clearInterval(interval);
  }, [currentIndex]);

  return (
    <div className="carousel">
      <img
        src={images[currentIndex]}
        alt="carousel"
        className="carousel-img"
      />

      <button className="nav left" onClick={prevImage}>❮</button>
      <button className="nav right" onClick={nextImage}>❯</button>

      <div className="dots">
        {images.map((_, i) => (
          <span
            key={i}
            className={i === currentIndex ? "dot active" : "dot"}
            onClick={() => setCurrentIndex(i)}
          ></span>
        ))}
      </div>
    </div>
  );
}

export default Carousel;
```

# Carousel.css
```
.carousel {
  position: relative;
  width: 600px;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0,0,0,0.2);
}

/* Image */
.carousel-img {
  width: 100%;
  height: 400px;
  object-fit: cover;
  transition: transform 0.5s;
}

.carousel-img:hover {
  transform: scale(1.05);
}

/* Buttons */
.nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0,0,0,0.5);
  color: white;
  border: none;
  padding: 12px;
  font-size: 22px;
  cursor: pointer;
  border-radius: 50%;
}

.left { left: 15px; }
.right { right: 15px; }

/* Dots */
.dots {
  position: absolute;
  bottom: 15px;
  width: 100%;
  text-align: center;
}

.dot {
  height: 12px;
  width: 12px;
  margin: 5px;
  display: inline-block;
  background: rgba(255,255,255,0.6);
  border-radius: 50%;
  cursor: pointer;
}

.active {
  background: white;
  width: 18px;
  border-radius: 20px;
}
```

## OUTPUT

<img width="1313" height="740" alt="exp5" src="https://github.com/user-attachments/assets/90e1bab7-81b4-4bdb-9bc3-625db47b4a9b" />

<img width="1077" height="706" alt="exp 5" src="https://github.com/user-attachments/assets/acfb5827-03a4-46c4-940b-47f331693b8f" />

## RESULT
The program for creating Image Carousel using React is executed successfully.
