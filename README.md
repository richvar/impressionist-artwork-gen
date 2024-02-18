# Impressionist Artwork Generation with StyleGAN2-ADA

![Interpolation-gif](https://github.com/richvar/random-hosting-github-bypass/blob/main/interpolation_movie(1).gif)


Using [Nvidia's StyleGAN2-ADA architecture](https://github.com/NVlabs/stylegan2-ada), I trained a GAN to generate Impressionist artworks based on a dataset of ~4,000 images at 1024x1024 resolution. 

## See this in action at [thismonetdoesnotexist.com](https://www.thismonetdoesnotexist.com)

## Training

I began by scraping WikiArt.org for paintings marked under Impressionism using a scraper created by robbiebarat, linked [here](https://github.com/robbiebarrat/art-DCGAN/blob/master/genre-scraper.py). I scanned over the dataset and got rid of paintings that did not fit into what I was looking for (pictures of statues, renaissance style paintings, etc.) 

I was left with about 3,670 images that I then resized to 1024x1024 using ImageMagick with this command:
```bash
magick mogrify -resize 1024x1024! *.jpg
```

I ran into some trouble during the training process and found that the dataset needed to fit certain criteria; namely all photos being the same resolution and color space. I looked back to my dataset and ran using ImageMagick:
```bash
magick identify *.jpg
```

This output a list of all images in the folder and their attributes. I was able to make sure all images resized correctly to 1024x1024 and searched for "gray". Every image with its colorspace listed as "Grayscale" instead of "sRGB" was then deleted. Training worked perfectly from this point on. 

I opted to train the GAN through Google Colab with a template shown [here](https://github.com/Hephyrius/Stylegan2-Ada-Google-Colab-Starter-Notebook), which allows for running code using Google GPUs and SSDs each in exchange for having to restart your runtime every so often. I would restart my runtime until I was connected to a Tesla V100 for more efficient training. The model was trained for about 5 days.

## Possible Improvements to Training
While landscapes look great, portraits leave something to be desired. In a later iteration of this project, I would either take out portraits entirely or standardize them (all looking the same way, head in same position in frame) for better results. 

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.
