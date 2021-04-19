# Impressionist Artwork Generation with StyleGAN2-ADA

Include thing here with morphing training gif with title, eye catching

Using [Nvidia's StyleGAN2-ADA architecture](https://github.com/NVlabs/stylegan2-ada), I trained a GAN to generate Impressionist artworks based on a dataset of ~4,000 images at 1024x1024 resolution. 

## [Click here to open Google Colab to generate your own artworks.](https://colab.research.google.com/drive/1rmR026gTGRpxITKUvDGvfH_gi7zC2Bq7?usp=sharing)

## Artwork gallery:

<details>
  <summary>Exhibit 1</summary>
<img src="https://imgur.com/UhUqXIc"/>
</details>

## Training

I began by scraping WikiArt.org for paintings marked under Impressionism using a scraper created by robbiebarat, linked [here](https://github.com/richvar/art-DCGAN/blob/master/genre-scraper.py). I scanned over the dataset and got rid of paintings that did not fit into what I was looking for (pictures of statues, renaissance style paintings, etc.) 

I was left with about 3,670 images that I then resized to 1024x1024 using ImageMagick with this command:
```bash
magick mogrify -resize 1024x1024! *.jpg
```

I ran into some trouble during the training process and found that the dataset needed to fit certain criteria: being all the same resolution and the same color space. I looked back to my dataset and run this command using ImageMagick:
```bash
magick identify *.jpg
```

This output a list of all images in the folder I pointed it to and their attributes. I was able to make sure all images resized correctly to 1024x1024 and ctrl-f'ed inside the terminal for the term "gray". Every image with its colorspace listed as "Grayscale" instead of "sRGB" was then deleted. Training worked perfectly from this point on. 

I opted to train the GAN through Google Colab with a template shown [here](https://github.com/Hephyrius/Stylegan2-Ada-Google-Colab-Starter-Notebook), which allows for running code using Google GPUs and SSDs each in exchange for having to restart your runtime every so often. I would restart my runtime until I was connected to a Tesla V100 for more efficient training. The model was trained for about 4 days, going through about [insert kimg here].

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.
