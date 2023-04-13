iOS-Depth-Effect-Wallpaper-Experiments
======================================

iOS 16 introduces depth effect wallpapers for the lock screen, where parts of the subject in the picture may overlap the clock.
This feature is enabled if can distinguish the subject and the background with some confidence.

However, if it can't, it simply disables the Depth Effect option.
There is no way to tune the algorithm, so you will need to **tune the image**, if you really want to make it work.
As Apple does not reveal how it works, it's basically a lot of hacking and trials.

This repo contains my notes and samples tinkering with it. Pull requests are welcomed! 

Note that there is no guarantee that a specific image may work. 
You will likely need knowledge of Photoshop or other image processing tools.
For basic knowledge of the Depth Effect (e.g. why the option is grey out), please search on the Internet.

## Test Platform
iPhone Xs, iOS 16.3.1

## Samples
Each sample directory contains individual README.

* [Zermatt](Zermatt)
* [CSM-Power](CSM-Power)
* [SG-Kurisu](SG-Kurisu)

NOTICE: These samples are only used to assist the explanation and are copyrighted by the original authors.

## Known Facts/Guesses
1. iOS uses an AI-based algorithm to detect the subject. It may be the same algorithm for subject selection in Photos (when you long press), but the confidence bar is certainly higher. 
> Example: [CSM-Power/original](https://www.pixiv.net/en/artworks/87469406), Photos is able to detect the subject but Depth Effect is disabled.

1. Another criterion to enable Depth Effect may be the size of the subject. If the subject overlaps a lot with the clock even if the image is zoomed out, the option does not show.
> Example: [CSM-Power/Power-Lock-Screen.jpg](CSM-Power/Power-Lock-Screen.jpg) works. But with its margin cropped, it no longer works.

1. Natural photos seem to work better than images like illustrations. 
> Maybe Apple trains the algorithm mostly on shot photos.

1. Red/pink backgrounds seem to be worse than blue/green ones. 
> Maybe because natural images tend to have sky/natural scenes as the backgrounds.

1. Noise in the background negatively affects the detection algorithm.
> I once added artificial noise to the background of [CSM-Power/Power-Lock-Screen.jpg](CSM-Power/Power-Lock-Screen.jpg), and suddenly it stopped working. Also, the main step that makes [SG-Kurisu/Kurisu-Lock-Screen.jpg](SG-Kurisu/Kurisu-Lock-Screen.jpg) work was manually selecting the background and denoising + Gaussian blurring.

1. Too much artificial brightness/saturation difference between foreground and background may break the algorithm.
> Happened once when I applied filters on the subject in [SG-Kurisu/Kurisu-Lock-Screen.jpg](SG-Kurisu/Kurisu-Lock-Screen.jpg). Had to undo it.


## Tips
* Use JPG. The same image may work in JPG but not in PNG. The reason is unclear though.
* Leave enough margin around the subject (point 2 above).
* Denoise the background (point 4).
  * In Photoshop, Object Selection tool + Direct Selection tool + Magic Wand tool can be a good combination to select the background.
  * If needed, re-work the background, like [CSM-Power/Power-Lock-Screen.jpg](CSM-Power/Power-Lock-Screen.jpg).
* Once you have a working version, make adjustments little by little and test frequently. Sometimes the Depth Effect option is just suddenly gone and you will have no idea which adjustment(s) cause it...