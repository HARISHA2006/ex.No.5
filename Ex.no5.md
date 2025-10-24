# Ex05 Image Carousel
## Date:24.10.25

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
## ImageCarousel.jsx
```
import React, { useState, useEffect } from 'react';
import './ImageCarousel.css';

const images = [
  'https://picsum.photos/id/1015/800/400',
  'https://picsum.photos/id/1016/800/400',
  'https://picsum.photos/id/1018/800/400',
  'https://picsum.photos/id/1020/800/400',
];

const ImageCarousel = ({ autoPlay = true, interval = 3000 }) => {
  const [currentIndex, setCurrentIndex] = useState(0);

  // Automatic slide change
  useEffect(() => {
    if (!autoPlay) return;
    const timer = setInterval(() => {
      setCurrentIndex((prev) => (prev + 1) % images.length);
    }, interval);
    return () => clearInterval(timer);
  }, [autoPlay, interval]);

  const goToNext = () => {
    setCurrentIndex((currentIndex + 1) % images.length);
  };

  const goToPrev = () => {
    setCurrentIndex((currentIndex - 1 + images.length) % images.length);
  };

  return (
    <div className="carousel-container">
      <div className="carousel-wrapper">
        <button className="arrow left" onClick={goToPrev}>
          &#10094;
        </button>
        <img
          src={images[currentIndex]}
          alt={`Slide ${currentIndex}`}
          className="carousel-image"
        />
        <button className="arrow right" onClick={goToNext}>
          &#10095;
        </button>
      </div>
      <div className="carousel-dots">
        {images.map((_, index) => (
          <span
            key={index}
            className={`dot ${currentIndex === index ? 'active' : ''}`}
            onClick={() => setCurrentIndex(index)}
          ></span>
        ))}
      </div>
    </div>
  );
};

export default ImageCarousel;
```

## ImageCarousel.css

```
body {
  margin: 0;
  padding: 0;
  font-family: 'Inter', sans-serif;
  height: 100vh;
  display: flex;
  justify-content: center; /* horizontal center */
  align-items: center;     /* vertical center */
  background: #f0f4f8;
}

.carousel-container {
  max-width: 800px;
  width: 100%;
  position: relative;
  text-align: center;
}

.carousel-wrapper {
  position: relative;
  overflow: hidden;
  border-radius: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.carousel-image {
  width: 100%;
  height: auto;
  display: block;
  transition: transform 0.5s ease;
}

.arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 2rem;
  background: rgba(0,0,0,0.3);
  color: #fff;
  border: none;
  padding: 0.5rem 1rem;
  cursor: pointer;
  border-radius: 50%;
  user-select: none;
  z-index: 2;
}

.arrow.left {
  left: 10px;
}

.arrow.right {
  right: 10px;
}

.arrow:hover {
  background: rgba(0,0,0,0.6);
}

.carousel-dots {
  margin-top: 10px;
}

.dot {
  height: 12px;
  width: 12px;
  margin: 0 4px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.dot.active {
  background-color: #717171;
}

```

## App.jsx
```
import React from 'react';
import ImageCarousel from './ImageCarousel';

function App() {
  return (
    <div>
      <h1 style={{textAlign: 'center', marginTop: '1rem'}}>React Image Carousel</h1>
      <ImageCarousel autoPlay={true} interval={4000} />
    </div>
  );
}

export default App;

```


## OUTPUT

<img width="1918" height="1078" alt="Screenshot 2025-10-24 160403" src="https://github.com/user-attachments/assets/6c4d8579-27dc-4f00-80e3-ee31b110db76" />

<img width="1916" height="1076" alt="Screenshot 2025-10-24 160439" src="https://github.com/user-attachments/assets/b7a7e461-10d1-4c0d-a98c-231bcb686666" />

<img width="1914" height="1079" alt="Screenshot 2025-10-24 160425" src="https://github.com/user-attachments/assets/f5bafee3-fdd4-47c2-95e6-aa8c92ebf382" />


<img width="1917" height="1077" alt="Screenshot 2025-10-24 160502" src="https://github.com/user-attachments/assets/ec23346d-8da5-4df4-af38-9f6826587615" />

## RESULT
The program for creating Image Carousel using React is executed successfully.
