Liri Blog
=========

This Liri Blog is based on [Jekyll](https://jekyllrb.com/).

You can see it online at [blog.liri.io](https://blog.liri.io/).

Layout and style are inspired by [Medium](https://medium.com/liridev),
[Google Blog](https://www.blog.google) and [Google Design](https://design.google).

The code was initially based upon [@elementary/blog-template](https://github.com/elementary/blog-template).

## Editing workflow

Fork this repository and send a pull request.

## How to handle images

Put images in the `images/` directory with a folder name that matches the post slug.
Image sizes should be:

 * Up to 800px wide for normal-width loDPI
 * Up to 1600px wide for normal-width HiDPI
 * Up to 800px for half- or third-width images on loDPI
 * Up to 1600px wide for half- or third-width images on HiDPI
 * 2560px wide for full-bleed

When scaling down, use a high quality interpolator like Sinc (Lanczos3) or NoHalo
in GIMP to avoid too much blur/fuzziness.

Name your sized images something sane like `image-name_800.jpg` for the loDPI version,
and `image-name_1600.jpg` for the HiDPI version. When writing the markdown, use this format:

```
![Alt Text]({{ site.baseurl }}/images/post-name/image-name_800.jpg){: srcset="{{ site.baseurl }}/images/post-name/image-name_1600.jpg 2x"}
```

Optimize images with the lowest JPG percent that looks good (i.e. manually in GIMP), and use something
like [Image Optimizer](https://appcenter.elementary.io/com.github.gijsgoudzwaard.image-optimizer) for PNGs.

Also consider JPGs instead of PNGs when the majority of the image is photographic or a gradient (i.e. not solid colors),
as that will compress way better than a PNG.

## Building and running locally

The blog is a simple Jekyll-powered site hosted by GitHub Pages. To run it locally,
see [the GitHub docs](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll/).

## Initial setup

First make sure Ruby is installed.

On Fedora systems you can install it this way:

```sh
sudo dnf install -y ruby-devel rubygems
```

We want to manually install gems in our home directory.

Add these to your `~/.bashrc`:

```
export GEM_HOME=$HOME/.gem
export PATH=$GEM_HOME/bin:$PATH
```

Now create the directory:

```sh
mkdir $HOME/.gem
```

Reload the environment:

```sh
source ~/.bashrc
```

Install the following stuff:

```sh
gem install bundler
cd blog
bundle install
```

## Serve

Serve the pages locally with:

```sh
cd blog
bundle exec jekyll serve --host 0.0.0.0
```

The site should now be available at [http://0.0.0.0:4000/](http://0.0.0.0:4000/) on your local machine,
and your local machine's IP address on your network—great for testing on mobile OSes.

### Drafts and future posts

Append `--drafts` to the serve command, and drafts in the `_drafts` folder will show up
based on their last-edited time. Similarly, append `--future` to the serve command to show future posts.
