# swiperJs_multiple_Instance
Multiple Instances of SwiperJs on the same page with the same settings

Creating two or more Sliders instances using the SwiperJs library is a fairly straightforward task. You can literally give your sliders different class names and then initialise them with JavaScript – please see the example below

## UPDATE: 
Swiper container element now should have class **swiper** instead of **swiper-container**.

        <div class="swiper-container-1 swiper">
           <div class="swiper-slide">Slide 1</div>
           <div class="swiper-slide">Slide 2</div>
           <div class="swiper-slide">Slide 3</div>
        </div>
        <div class="swiper-container-2 swiper">
           <div class="swiper-slide">Slide 1</div>
           <div class="swiper-slide">Slide 2</div>
           <div class="swiper-slide">Slide 3</div>
        </div>

        <script>
        var swiper1 = new Swiper('.swiper-container-1', { /* Options */ })
        var swiper2 = new Swiper('.swiper-container-2', { /* Options */ })
        </script

## What if we needed to create two or more sliders with the same options?
The most apparent and lazy way would be to keep replicating the code above and add as many sliders as you need. If you have a few sliders as I did in my project than it might be a bad idea for obvious reasons.

I actually found some really good answers on this GitHub Issues page, but everything was done with jQuery which wasn’t an option for me. So I took the best of the answers and just converted everything to vanilla JavaScript. It was fairly easy to convert the jQuery code to vanilla JavaScript, but I wanted to share the code with you so you can save some time.

 ## Solution
Create a few sliders with the same class name of **swiper-container** ( you can add as many as you want). Your code should look similar to mine:

        <div class="swiper-container swiper">
           <div class="swiper-slide">Slide 1</div>
           <div class="swiper-slide">Slide 2</div>
           <div class="swiper-slide">Slide 3</div>
        </div>
        <div class="swiper-container swiper">
           <div class="swiper-slide">Slide 1</div>
           <div class="swiper-slide">Slide 2</div>
           <div class="swiper-slide">Slide 3</div>
        </div>
        <div class="swiper-container swiper">
           <div class="swiper-slide">Slide 1</div>
           <div class="swiper-slide">Slide 2</div>
           <div class="swiper-slide">Slide 3</div>
        </div>

        **Javascript**
        const myCustomSlider = document.querySelectorAll('.swiper-container');
        for( i=0; i< myCustomSlider.length; i++ ) {          
            myCustomSlider[i].classList.add('swiper-container-' + i);        
              var slider = new Swiper('.swiper-container-' + i, {
                   /* Options */
              });        
        }
That’s it.

## Other – Adding thumbs
Quick thumbs example. (This will be formatted better as soon as I get the chance)


    <div class="swiper-container swiper gallery-top">
        <div class="swiper-wrapper">
            <div class="swiper-slide" style="background-image:url('https://u8x3b4g8.stackpathcdn.com/wp-content/uploads//2020/12/minimalistic-website-design-mockup_compressed.jpg')"></div>
            <div class="swiper-slide" style="background-image:url('https://u8x3b4g8.stackpathcdn.com/wp-content/uploads//2020/12/minimalistic-website-design-mockup_compressed.jpg')"></div>
        </div>  
    </div>
    <div class="swiper-container swiper gallery-thumbs thumbs-class">
        <div class="swiper-wrapper">
            <div class="swiper-slide" style="background-image:url('https://u8x3b4g8.stackpathcdn.com/wp-content/uploads//2020/12/minimalistic-website-design-mockup_compressed.jpg')"></div>
            <div class="swiper-slide" style="background-image:url('https://u8x3b4g8.stackpathcdn.com/wp-content/uploads//2020/12/minimalistic-website-design-mockup_compressed.jpg')"></div>
        </div>
    </div>

    <div class="swiper-container swiper gallery-top">
        <div class="swiper-wrapper">
            <div class="swiper-slide" style="background-image:url('https://u8x3b4g8.stackpathcdn.com/wp-content/uploads//2020/11/swiper-js-multiple-instances_compressed.jpg')"></div>
            <div class="swiper-slide" style="background-image:url('https://u8x3b4g8.stackpathcdn.com/wp-content/uploads//2020/12/minimalistic-website-design-mockup_compressed.jpg')"></div>
        </div>  
    </div>
    <div class="swiper-container swiper gallery-thumbs thumbs-class">
        <div class="swiper-wrapper">
        <div class="swiper-slide" style="background-image:url('https://u8x3b4g8.stackpathcdn.com/wp-content/uploads//2020/11/swiper-js-multiple-instances_compressed.jpg')"></div>
        <div class="swiper-slide" style="background-image:url('https://u8x3b4g8.stackpathcdn.com/wp-content/uploads//2020/12/minimalistic-website-design-mockup_compressed.jpg')"></div>
        </div>
    </div>


      <!-- Initialize Swiper -->
      <script>
          const myCustomSlider = document.querySelectorAll('.gallery-top');
          const myCustomGalleryThumbs = document.querySelectorAll('.thumbs-class');
      
          for (i = 0; i < myCustomSlider.length; i++) {
              myCustomSlider[i].classList.add('gallery-top-' + i);
              myCustomGalleryThumbs[i].classList.add('thumbs-class-' + i);
      
              var galleryThumbs = new Swiper('.thumbs-class-' + i , {
                  spaceBetween: 10,
                  slidesPerView: 4,
                  freeMode: true,
                  watchSlidesVisibility: true,
                  watchSlidesProgress: true,
              });
      
              var galleryTop = new Swiper('.gallery-top-' + i, {
                  spaceBetween: 10,
                  thumbs: {
                      // el: '.thumbs-class',
                      // slidesPerView: 5,
                      swiper: galleryThumbs
                  }
              });
          }
      </script>
