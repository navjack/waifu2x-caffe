# waifu2x-caffe (for Windows)
----------

Creator: lltcggie

This software only converts the conversion function of the image conversion software "[waifu2x](https://github.com/nagadomi/waifu2x)
It was rewritten using [Caffe](http://caffe.berkeleyvision.org/) and built for Windows.
Although it can convert with CPU, using CUDA (or cuDNN) can convert faster than CPU.

GUI supports English, Japanese, Simplified Chinese, Traditional Chinese, Korean, Turkish, and French.

You can download the software in the "Downloads" section of the [here releases page](https://github.com/lltcggie/waifu2x-caffe/releases).

## On this page

1. [I / O setting](#i-o-setting)
1. ["Input Path"](#input-path)
1. ["Output Path"](#output-path)
1. ["Extensions to convert within folders"](#extensions-to-convert-wit)
1. ["Output extension"](#output-extension)
1. ["Output image quality setting"](#output-image-quality-sett)
1. ["Number of output depth bits"](#number-of-output-depth-bi)
1. [Conversion Image Quality / Processing Setting](#conversion-image-quality-)
1. ["Conversion mode"](#conversion-mode)
1. ["JPEG noise removal level"](#jpeg-noise-removal-level)
1. ["Enlarged size"](#enlarged-size)
1. ["model"](#model)
1. ["Using TTA Mode"](#using-tta-mode)
1. [Processing speed setting](#processing-speed-setting)
1. ["split size"](#split-size)
1. [Operation setting](#operation-setting)
1. ["Automatic conversion start setting at file input setting"](#automatic-conversion-star)
1. ["Processor Used"](#processor-used)
1. ["Do not overwrite output file"](#do-not-overwrite-output-f)
1. ["Startup setting with argument"](#startup-setting-with-argu)
1. ["GPU No. used"](#gpu-no-used)
1. ["Input reference fixed folder"](#input-reference-fixed-fol)
1. ["Fixed folder when referring to output"](#fixed-folder-when-referri)
1. [Other](#other)
1. ["UI language"](#ui-language)
1. ["cuDNN check"](#cudnn-check)
1. [-l , --input_extension_list](#l-input_extension_list)
1. [-e , --output_extention](#e-output_extention)
1. [- m , --mode](#m-mode)
1. [-s , --scale_ratio](#s-scale_ratio)
1. [- w , --scale_width](#w-scale_width)
1. [- h , --scale_height](#h-scale_height)
1. [- n , - noise_level](#n-noise_level)
1. [- p , - process](#p-process)
1. [- c , --crop_size](#c-crop_size)
1. [- q , --output_quality](#q-output_quality)
1. [- d , --output_depth](#d-output_depth)
1. [- b , - batch_size](#b-batch_size)
1. [- gpu](#gpu)
1. [- t , - tta](#t-tta)
1. [-, --ignore_rest](#ignore_rest)
1. [-o , --output_folder](#o-output_folder)
1. [--auto_start](#auto_start)
1. [--auto_exit](#auto_exit)
1. [- no overwrite](#no-overwrite)
1. [--version](#version)
1. [- ?, --help](#help)
1. [-i , --input_file](#i-input_file)
1. [-o , --output_file](#o-output_file)
1. [--model_dir](#model_dir)
1. [--crop_w](#crop_w)
1. [--crop_h](#crop_h)
1. [See also](#see-also)


## Required environment
----------

In order to operate this software, at least the following environment is necessary.

- OS: Windows Vista and later 64bit (There is no exe for 32bit)
- Memory: Free memory 1 GB or more (depending on the image size to be converted)
- GPU: NVIDIA GPU with Compute Capability 2.0 or higher (not required when converting with CPU)
- Visual C ++ 2013 redistributable package installed (required)
	- The above package is [here](https://www.microsoft.com/en-US/download/details.aspx?id=40784)
	- After pressing the `download` button, select `vcredist_x64.exe` and download and install it.
	- If you can not find it, try searching "Visual C ++ 2013 redistributable package".

When converting with cuDNN, further

- GPU: NVIDIA GPU with Compute Capability 3.0 or higher

If you want to know the Compute Capability of your GPU, please check [this page](https://developer.nvidia.com/cuda-gpus).

## About cuDNN
--------

cuDNN is a library for high-speed machine learning which can be used only with NVIDIA GPU.
Although you can convert with CUDA without using cuDNN, using cuDNN has the following advantages.

- Depending on the type of GPU used, you can convert images faster
- You can reduce the usage of VRAM (at least at less than half of CUDA, the difference opens as the division size increases)

CuDNN has such advantages, but because of license it can not distribute necessary files for operation.
So people who want to use cuDNN download binary for Windows (v 5.1 RC or later) on [this page](https://developer.nvidia.com/cuDNN)
Please put "cudnn64_7.dll" in the folder of waifu2x-caffe.
If you insert dll while software is running, please restart the software.
(To download cuDNN you need to register with NVIDIA Developer and register with CUDA Registered Developers.
 CUDA Registered Developers probably has a (simple) review, so it does not mean that you can download cuDNN immediately after you register. )

Measurement results of processing speed and VRAM usage in the author's environment are as follows.

- GPU: GTX 980 Ti
- VRAM: 6 GB
- Processing content: PNG 4ch image with 1000 * 1000 noise removal and enlargement, JPEG noise removal level 1, magnification factor 2.00, TTA mode unused
- Processing time measurement method: Measured average processing time of 10 times in CUI version. However, processing is done twice in advance at first (in order not to include the time required for initialization)
- Calculation method of VRAM usage: (Maximum VRAM used during processing in GUI version) - (VRAM usage after starting GUI version)

cuDNN RGB model

| Split size |	Processing time   |   VRAM usage (MB)			|
|:-----------|:-------------------|:----------------------------|
| 100		 | 00:00:03.170 	  | 278				 			|
| 125		 | 00:00:02.745 	  | 279				 			|
| 200		 | 00:00:02.253 	  | 365				 			|
| 250		 | 00:00:02.147 	  | 446				 			|
| 500		 | 00:00:01.982 	  | 1110						|

CUDA RGB model

| Split size |	Processing time   |   VRAM usage (MB)			|
|:-----------|:-------------------|:----------------------------|
| 100		 | 00:00:06.192 	  | 724							|
| 125		 | 00:00:05.504 	  | 724							|
| 200		 | 00:00:04.642 	  | 1556						|
| 250		 | 00:00:04.436 	  | 2345						|
| 500		 | Unmeasurable		  | Unmeasurable (6144 or more) |

cuDNN UpRGB model

| Split size |	Processing time   |   VRAM usage (MB)			|
|:-----------|:-------------------|:----------------------------|
| 100		 | 00:00:02.831 	  | 328							|
| 125		 | 00:00:02.573 	  | 329							|
| 200		 | 00:00:02.261 	  | 461							|
| 250		 | 00:00:02.150 	  | 578							|
| 500		 | 00:00:01.991 	  | 1554						|

CUDA UpRGB model

| Split size |	Processing time   |   VRAM usage (MB)			|
|:-----------|:-------------------|:----------------------------|
| 100		 | 00:00:03.669 	  | 788							|
| 125		 | 00:00:03.382 	  | 787							|
| 200		 | 00:00:02.965 	  | 1596						|
| 250		 | 00:00:02.852 	  | 2345						|
| 500		 | Unmeasurable		  | Unmeasurable (6144 or more) |

## Usage (GUI version)
--------

"Waifu2x - caffe.exe" is GUI software. Double click to start.
Or you can drag and drop files and folders to "waifu2x-caffe.exe" in Windows Explorer and convert with the setting at the last boot.
In that case, depending on the setting, the dialog is automatically closed when conversion is successful.
Also, you can set options on the command line using the GUI.
For details, please read the command line option (common) and command line option (GUI version).

After launch, if you drag and drop images or folders into the "Input Path" column, the "Output Path" field will be set automatically.
If you want to change the output destination, please change the "output path" field.

You can change the conversion setting according to your preference.

## <a id="i-o-setting" href="#i-o-setting">I / O setting</a>
This is a set of setting items related to file input / output.

## <a id="input-path" href="#input-path">"Input Path"</a>
Specify the path of the file you want to convert.
If you specify a folder, convert the file with the "extension to convert within the folder" including the subfolder.
You can specify multiple files and folders by dragging.
In that case, it will be output in the new folder keeping the file and folder structure.
("(Multi Files)" is displayed in the input pass column.The output folder name is generated from the file and the folder name grasped with the mouse)
When selecting a file by pressing the Browse button, you can select a single file, folder, or multiple files.

## <a id="output-path" href="#output-path">"Output Path"</a>
Specify the path to save the converted image.
If you specify a folder in "Input path", save the converted file in the specified folder (without changing the folder structure). If there is no specified folder, it will be created automatically.

## <a id="extensions-to-convert-wit" href="#extensions-to-convert-wit">"Extensions to convert within folders"</a>
When the "input path" is a folder, specify the extension of the image to be converted in the folder.
The default value is `png: jpg: jpeg: tif: tiff: bmp: tga`.
The delimiter is `:`.
Capital letters and lower case letters are not distinguished.
Eg. Png: jpg: jpeg: tif: tiff: bmp: tga

## <a id="output-extension" href="#output-extension">"Output extension"</a>
Specify the format of the converted image.
Values ​​that can be set for "Output image quality setting" and "Number of output depth bits" differ depending on the format specified here.

## <a id="output-image-quality-sett" href="#output-image-quality-sett">"Output image quality setting"</a>
Specify the image quality of the converted image.
Values ​​that can be set are integers.
The range and meaning of possible values ​​depend on the format set in "Output extension".

- .jpg: Range of values ​​(0 to 100) The higher the number, the higher the image quality
- .webp: Range of values ​​(1 to 100) If the number is high and the image quality is 100, lossless compression
- .tga: Value range (0 to 1) 0 indicates no compression, 1 indicates RLE compression

## <a id="number-of-output-depth-bi" href="#number-of-output-depth-bi">"Number of output depth bits"</a>
Specify the number of bits per channel of the converted image.
Values ​​that can be specified vary depending on the format set in "Output extension".

## <a id="conversion-image-quality-" href="#conversion-image-quality-">Conversion Image Quality / Processing Setting</a>
Processing method of file conversion, Setting items related to image quality.

## <a id="conversion-mode" href="#conversion-mode">"Conversion mode"</a>
Specify the conversion mode.

- Noise elimination and expansion: Noise elimination and expansion
- Expansion: We will expand
- Noise removal: Noise removal
- Noise elimination (automatic discrimination) and enlargement: Perform enlargement. It also performs noise removal only when the input is a JPEG image

## <a id="jpeg-noise-removal-level" href="#jpeg-noise-removal-level">"JPEG noise removal level"</a>
Specify the noise removal level. The higher level removes the noise more strongly, but there is also the possibility of becoming a slick picture.
## <a id="enlarged-size" href="#enlarged-size">"Enlarged size"</a>
Set the size after enlargement.

- Specified by enlargement ratio: Enlarges the image at the specified enlargement ratio
- Specified by the width after conversion: While enlarging the aspect ratio of the image, enlarge it so that it becomes the specified width (unit is pixel)
- Specified by the vertical width after conversion: While maintaining the aspect ratio of the image, enlarge it so that it becomes the designated vertical width (unit is pixel)
- Specified by width and width after conversion: Enlarges so that it becomes the specified vertical and horizontal width. Specify it like "1920 x 1080" (unit is pixel)

In the case of magnification ratios exceeding 2 times (in the case of removing noise, only the first one is performed), the enlargement ratio is doubled until exceeding the designated enlargement ratio, and in the case of the enlargement ratio not being a power of 2, We will do the process. Therefore, there is a possibility that the result of conversion will be a solid picture.

## <a id="model" href="#model">"model"</a>
Specify the model to use.
Since the optimum model differs depending on the image to be converted, we recommend trying various models.

- 2-dimensional illustration (RGB model): 2-dimensional illustration model for converting all RGB of image
- Photo · Anime (Photo model): Model for photography · animation
- 2 dimensional illustration (UpRGB model): A model that transforms at higher speed and equal or higher image quality than 2D illustration (RGB model). However, since the amount of memory (VRAM) consumed by the RGB model is large, adjust the partition size when forcibly terminating during conversion
- Photo · Animation (UpPhoto model): A model that converts with higher image quality than the photo / animation (Photo model) at high speed. However, since the amount of memory (VRAM) consumed by the Photo model is large, adjust the partition size when forcibly terminating during conversion
- 2-dimensional illustration (Y model): 2-dimensional illustration model that converts only the luminance of the image

## <a id="using-tta-mode" href="#using-tta-mode">"Using TTA Mode"</a>
Specify whether to use TTA (Test-Time Augmentation) mode or not.
If you use TTA mode, PSNR (image evaluation index) will rise about 0.15 instead of 8 times slower conversion.

## <a id="processing-speed-setting" href="#processing-speed-setting">Processing speed setting</a>
It is a set of setting items that affect the processing speed of image conversion.

## <a id="split-size" href="#split-size">"split size"</a>
Specify the width (in pixels) when processing is performed internally.
The best way to decide the numerical value (processing is the fastest) is explained in the section "Split size".
The upper one delimited by "-------" is the divisor of the vertical and horizontal sizes of the input image,
The lower one is a general-purpose division size read from "crop_size_list.txt".
If the partition size is too large, beware that the amount of memory required (the amount of VRAM when GPU is used) exceeds the memory available on the PC and the software terminates forcibly.
Since it affects the processing speed to a certain extent, when converting a large number of images with the same image size with folder specifications, we recommend that you convert after checking the optimum partition size.

## <a id="operation-setting" href="#operation-setting">Operation setting</a>
It is a group of settings that summarizes the behavior settings that seems to have little chance to change.

## <a id="automatic-conversion-star" href="#automatic-conversion-star">"Automatic conversion start setting at file input setting"</a>
It sets whether to automatically start converting when specifying an input file with reference button or drag and drop.
In the case where the input file is given as an argument to exe, the setting contents of this item will not be affected.

- Do not start automatically: Even if you enter a file, conversion will not start automatically
- Start with inputting even one file: Start converting automatically when you input even one file
- Start when you input a folder or multiple files: Start folder: When multiple files are input, conversion starts automatically. Please convert a single image file only when adjusting conversion settings

## <a id="processor-used" href="#processor-used">"Processor Used"</a>
Specify the processor that performs the conversion.

- CUDA (cuDNN if used): Convert using CUDA (GPU) (cuDNN is used if cuDNN is available)
- CPU: Convert using CPU only

## <a id="do-not-overwrite-output-f" href="#do-not-overwrite-output-f">"Do not overwrite output file"</a>
If this setting is ON, if there is a file with the same name in the image writing destination, no conversion will be done.

## <a id="startup-setting-with-argu" href="#startup-setting-with-argu">"Startup setting with argument"</a>
Sets the behavior when input file is given as argument to exe.

- Convert at startup: Conversion starts automatically at startup
- End on success: Automatically terminate unless conversion failed at the end of conversion

## <a id="gpu-no-used" href="#gpu-no-used">"GPU No. used"</a>
You can specify the device number to use when there are multiple GPUs. Ignored when in CPU mode or when an invalid device number is specified.

## <a id="input-reference-fixed-fol" href="#input-reference-fixed-fol">"Input reference fixed folder"</a>
Fix the folder displayed first when you press the input reference button to the folder set here.

## <a id="fixed-folder-when-referri" href="#fixed-folder-when-referri">"Fixed folder when referring to output"</a>
Fix the output destination folder of the converted image to the folder set here.
Also, fix the folder displayed first when you press the output reference button to the folder set here.

## <a id="other" href="#other">Other</a>
Other setting items group.

## <a id="ui-language" href="#ui-language">"UI language"</a>
Set the language of the UI.
The same language as the language setting of the PC is selected at the first start. (It will be in English if it does not exist)

## <a id="cudnn-check" href="#cudnn-check">"cuDNN check"</a>
You can check if you can use cuDNN by pressing "cuDNN check" button.
If cuDNN can not be used, the reason is displayed.

Click "Execute" button to start conversion.
If you want to cancel halfway, press "Cancel" button.
However, there is a time lag until actually stopping.
The progress bar shows the degree of progress when changing multiple images.
The expected remaining time is displayed in the log, but this is an estimate when processing multiple files of the same vertical width and horizontal width.
So it is not useful when the size of the file falls apart, and only "unknown" is displayed when the number of processed images is 2 or less.

## How to use (CUI version)
--------

"Waifu2x - caffe - cui.exe" is a command line tool.
Start `command prompt` and type in the command as follows.


The following commands output usage on the screen.
`` `
waifu2x-caffe-cui.exe --help
`` `

The following commands are examples of commands that perform image conversion.
`` `
waifu2x-caffe-cui.exe -i mywaifu.png -m noise_scale --scale_ratio 1.6 - noise_level 2
`` `
When you do the above, the conversion result is saved in `mywaifu (noise_scale) (Level 2) (x 1.600000) .png`.

For details of the command list and each command, please read the command line option (common) and command line option (CUI version).

## Command line option (common)
--------

With this software, the following options can be specified.
In the GUI version, when starting with a command line option other than the input file specified, the option file is not saved currently.
Also, options not specified in the GUI version are used at the time of last exit.

## <a id="l-input_extension_list" href="#l-input_extension_list">-l , --input_extension_list</a>
When input_file is a folder, specify the extension of the image to be converted in the folder.
The default value is `png: jpg: jpeg: tif: tiff: bmp: tga`.
The delimiter is `:`.
Eg. Png: jpg: jpeg: tif: tiff: bmp: tga

## <a id="e-output_extention" href="#e-output_extention">-e , --output_extention</a>
When input_file is a folder, specify the extension of the output image.
The default value is `png`.

## <a id="m-mode" href="#m-mode">- m , --mode</a>
Specify the conversion mode. If not specified, `noise_scale` is selected.

- noise: Performs noise removal (to be exact, image conversion is performed using a noise removal model)
- scale: Enlarges (exactly, after enlarging with the existing algorithm, image conversion is performed using the model for complementing enlarged image)
- noise_scale: Performs noise elimination and enlargement (enlargement processing is continued after removing noise)
- auto_scale: Enlarges. It also performs noise removal only when the input is a JPEG image

## <a id="s-scale_ratio" href="#s-scale_ratio">-s , --scale_ratio</a>
Specify how many times the image is enlarged. The default value is `2.0`, but you can specify anything other than 2.0 times.
If scale_width or scale_height is specified, that will take precedence.
If you specify a number other than 2.0, the following processing is performed.
* First of all, repeat double enlargement so as to cover the specified magnification sufficiently.
If a number other than the power of 2 is specified, the image enlarged so that it becomes the designated magnification is reduced by a linear filter.

## <a id="w-scale_width" href="#w-scale_width">- w , --scale_width</a>
While keeping the aspect ratio of the image, enlarge it to the specified horizontal width (unit is pixel).
When it is specified together with scale_height, the image is enlarged so that it becomes the specified vertical and horizontal width.

## <a id="h-scale_height" href="#h-scale_height">- h , --scale_height</a>
While maintaining the aspect ratio of the image, enlarge it to the specified vertical width (unit is pixel).
When it is specified together with scale_width, it enlarges the image so that it becomes the specified vertical and horizontal width.

## <a id="n-noise_level" href="#n-noise_level">- n , - noise_level</a>
Specify the noise removal level. Since only the levels 0 to 3 are prepared for the noise removal model,
Please specify 0, 1, 2 or 3.
The default value is `0`.

## <a id="p-process" href="#p-process">- p , - process</a>
Specify the processor to use for processing. The default value is `gpu`.

- cpu: Convert using CPU.
- gpu: Convert using CUDA (GPU). For Windows version only use cuDNN if you can use cuDNN.
- cudnn: Convert using cuDNN.

## <a id="c-crop_size" href="#c-crop_size">- c , --crop_size</a>
Specify the division size. The default value is `128`.

## <a id="q-output_quality" href="#q-output_quality">- q , --output_quality</a>
Set the image quality of the converted image. The default value is `-1`
Specifiable values ​​and meanings depend on the format set in "Output extension".
If -1, default values ​​for each image format are used.

## <a id="d-output_depth" href="#d-output_depth">- d , --output_depth</a>
Specify the number of bits per channel of the converted image. The default value is `8`.
Values ​​that can be specified vary depending on the format set in "Output extension".

## <a id="b-batch_size" href="#b-batch_size">- b , - batch_size</a>
Specify the mini-batch size. The default value is `1`.
The mini-batch size is the number of simultaneous processing of blocks obtained by dividing an image by "division size". For example, if you specify `2`, it will convert two blocks at a time.
mini-batch Increasing the size increases the GPU usage rate as well as increasing the split size, but if you feel it is measured, it is more effective to increase the split size.
(For example, if you set split size to `128` and mini-batch size to` 1` rather than split size set to `64` and mini-batch size to` 4`, processing will be finished faster)

## <a id="gpu" href="#gpu">- gpu</a>
Specify the GPU device number to be used for processing. The default value is `0`.
Please note that the GPU device number starts with 0.
Ignored if you do not use GPU for processing.
Also, if you specify a GPU device number that does not exist, it will be executed with the default GPU.

## <a id="t-tta" href="#t-tta">- t , - tta</a>
If `1` is specified, TTA mode is used. The default value is `0`.

## <a id="ignore_rest" href="#ignore_rest">-, --ignore_rest</a>
Ignores all options after this option is specified.
It is for script batch file.

## Command line option (GUI version)
--------

In the GUI version, arguments that do not fit option specifications are recognized as input files.
You can specify files, folders, multiple files, and files and folders at the same time as input files.

## <a id="o-output_folder" href="#o-output_folder">-o , --output_folder</a>
Set the path to the folder where the converted image will be saved.
Save the converted file in the specified folder.
The naming convention of the converted file is the same as the output file name automatically determined when setting the input file in the GUI.
If it is not specified, it is saved in the same folder as the first input file.

## <a id="auto_start" href="#auto_start">--auto_start</a>
If `1` is specified, conversion is started automatically at startup.

## <a id="auto_exit" href="#auto_exit">--auto_exit</a>
If you specify `1`, it automatically ends when the conversion succeeds if it is automatically converted at startup.

## <a id="no-overwrite" href="#no-overwrite">- no overwrite</a>
If `1` is specified, if there is a file with the same name in the image writing destination, no conversion will be done.

upconv_7_photo | anime_style_art_ rgb | photo | anime_style_art_y>
Specify the model to use.
It corresponds to the setting item "model" in the GUI as follows.

- upconv_7_anime_style_art_ rgb: 2D illustration (UpRGB model)
- upconv_7_photo: Photography · Anime (UpPhoto model)
- anime_style_art_rgb: 2D illustration (RGB model)
- photo: Photo · Anime (Photo model)
- anime_style_art_y: 2-dimensional illustration (Y model)

## Command line option (CUI version)
--------

## <a id="version" href="#version">--version</a>
Output version information and exit.

## <a id="help" href="#help">- ?, --help</a>
Display usage and exit.
Please feel free to check how to use.

## <a id="i-input_file" href="#i-input_file">-i , --input_file</a>
(Required) Path to the image to be converted
If you specify a folder, it will convert all image files below that folder and output to the folder specified by output_file.

## <a id="o-output_file" href="#o-output_file">-o , --output_file</a>
Path to the file to save the converted image
(When input_file is a folder) Path to the folder where the converted image is saved
(When input_file is an image file) Please be sure to input the extension (last .png etc.).
If not specified, the file name is automatically determined and saved in that file.
The file name determination rule is
`` (Original image file name) `` (model name) `` (mode name) `` (noise removal level (in noise removal mode)) `` (magnification scale in magnified mode) `` Number of bits (except for 8 bits)) `` Output extension `
It has become like.
Basically, the saved location is the same directory as the input image.

## <a id="model_dir" href="#model_dir">--model_dir</a>
Specify the path to the directory where the model is stored. The default value is `models / upconv_7_anime_style_art_rgb`.
The following models are included with the standard.

- `models / anime_style_art_rgb`: 2-dimensional image model for converting all RGB
- `models / anime_style_art`: model for two-dimensional image that converts only luminance
- `models / photo`: Photos that convert all RGB, models for animated images
- `models / upconv_7_anime_style_art_rgb`: Anime_style_art_rgb A model to convert at higher speed and equal or higher image quality
- `models / upconv_7_photo`: A model that converts with higher image quality than the photo at higher speed
- `models / ukbench`: old-fashioned model for photography (only models that are enlarged are attached, noise can not be removed)

Basically it does not have to be specified. Please specify it when using a model other than the default or your own model.

## <a id="crop_w" href="#crop_w">--crop_w</a>
Specify the division size (width). If not set, the value of crop_size is used.
Specifying the divisor of the width of the input image may make it possible to convert faster.

## <a id="crop_h" href="#crop_h">--crop_h</a>
Specify the division size (vertical width). If not set, the value of crop_size is used.
Specifying the divisor of the vertical width of the input image may make it possible to convert it faster.

## Split size
--------

When waifu 2x-caffe (waifu 2 x is also) converts the image,
We divide the image into pieces of a certain size, convert one by one, and finally combine them to return them to a single image.
The split size (crop_size) is the width (in pixels) when splitting this image.

If the GPU is not fully used even when converting with CUDA (the GPU usage rate has not reached 100%),
Increasing this number may cause processing to be completed quickly. (Because it will be possible to use up GPU)
Please adjust while watching GPU Load (GPU usage) and Memory Used (VRAM usage) at [GPU - Z](http://www.techpowerup.com/gpuz/).
In addition, please refer to it because it has the following characteristics.

- The higher the number is, the more it will not become faster
- If the division size is a divisor of the vertical and horizontal sizes of the image (or a small number when it is divided), the amount of computation wastefully decreases and becomes faster. (There seems to be the case that the numerical value that does not fit much with this condition becomes the fastest?
- If you doubled the number, in theory the amount of memory used will be quadrupled (actually 3 to 4 times etc) so be careful not to drop the software. Especially since CUDA consumes more memory than cuDNN, be careful

## About images with alpha channel
--------

With this software, expansion of images with alpha channel is also supported.
However, since it is processing to enlarge the alpha channel alone, please note that it takes about twice as long as the image without alpha channel does not expand.
However, when the alpha channel is composed of a single color, it can be enlarged in about the same time as when there is no alpha channel.

## The format of language files
--------

Language files format is JSON.
If you create new language file, add language setting to 'lang / LangList.txt'.
'lang / LangList.txt' format is TSV (Tab-Separated Values).

- LangName: Language name
- LangID: Primary language [See MSDN](https://msdn.microsoft.com/en-us/library/windows/desktop/dd318693.aspx)
- SubLangID: Sublanguage [See MSDN](https://msdn.microsoft.com/en-us/library/windows/desktop/dd318693.aspx)
- FileName: Language file name

ex.

- Japanese Lang ID: 0x11 (LANG_JAPANESE), SubLangID: 0x01 (SUBLANG_JAPANESE_JAPAN)
- English (US) LangID: 0x09 (LANG_ENGLISH), SubLangID: 0x01 (SUBLANG_ENGLISH_US)
- English (UK) LangID: 0x09 (LANG_ENGLISH), SubLangID: 0x02 (SUBLANG_ENGLISH_UK)

## Disclaimer
--------------

This software is not guaranteed.
Please use it under the judgment of the user.
The creator shall not bear any obligation.

## Acknowledgments
------
[Ultraist](https://twitter.com/ultraistter) who produced the original [waifu2x](https://github.com/nagadomi/waifu2x) and model and released it under the MIT license Mr.,
[Amigo](https://twitter.com/WL_Amigo) created [waifu2x-converter](https://github.com/WL-Amigo/waifu2x-converter-cpp) based on the original waifu2x Mr. (I was quite referring to how to write README and LICENSE.txt, how to use OpenCV, etc.)
will be grateful to.
Also, @ paul70078 who translated the message into English, @ yonhakcher who translated the message into Chinese (Simplified), @ mzhboy who gave a pull request for translation in Simplified Chinese,
@ Kenin 0726 who translated the message into Korean, @ aarhirin who suggested improvement of Korean translation,
@ Lizardon1995, @ yoonhakcher who translated the message into Chinese (traditional), @ Scharynche who gave a pull request for Turkish translation, @ Serted who gave a pull request for French translation,
Thanks to JYUNYA for providing GUI version icon.

## Change log
--------------

- ver 1.1.8.4
	- compatible with cuDNN v7

- ver 1.1.8.3
	- Fixed that the enlargement of vertical width or horizontal width specification may cause deviation of about 1px from specified size due to calculation error
	- Correct that output of CUI may be garbled in non-Japanese environment
	- compatible with cuDNN v6

- ver 1.1.8.2
	- Fixed a bug that sometimes caused errors when selecting output folder
	- Fixed a bug recognized as horizontal width specification even if vertical width size is specified in GUI
	- The output depth bit number can not be changed by input

- ver 1.1.8.1
	- Added size specification by width and width after conversion in GUI
	- CUI allows you to simultaneously specify width and width after conversion
	- French added to translate GUI

- ver 1.1.8
	- Updated CUDA Toolkit to 8.0.44 (dll included is also updated)
	- cu DNN v 5.1 compatible
	- If the alpha channel is monochromatic, speed up by expanding with cv :: INTER_NEAREST

- ver 1.1.7.1
	- Add icon to GUI version
	- Fixed a bug that output was wrong when using TTA mode when crop_w and crop_h are different values

- ver 1.1.7
	- Update upconv model
	- Change the model used by the standard to upconv_7_anime_style_art_rgb
	- The upconv model is displayed on the GUI version
	- Fixed a bug that the output file name does not change even when changing the noise removal level to 0 in the GUI version

- ver 1.1.6.1
	- Fixed a bug that denoising level 0 could not be specified with command line option
	- Fixed a bug that output file name suffix does not change when noise removal level 0 radio button is pressed in GUI version
	- Fixed bug that Chinese (simplified) translation was not displayed correctly

- ver 1.1.6
	- Add noise removal level 0
	- Change the default value of noise removal level from 1 to 0
	- Fixed a bug where vertical width specification enlargement behavior was the same as horizontal width specification
	- Fixed that the use amount of VRAM exceeding the maximum value was forcibly terminated in algorithm search using cuDNN
	- Fixed a bug that forcibly terminates when selecting a large number of files in GUI input input reference dialog
	- Fixed a bug that command line option crop size specification was not working in GUI version
	- Correct that strange images appear when converting 32 bit Bitmap

- ver 1.1.5
	- Added upconv model (photo)
	- Photo Noise Reduction Model Update
	- compatible with cuDNN v5.1 RC
	- Faster processing speed when using cuDNN (we made cu DNN usage algorithm fastest and cached the result)
	- Added crop_w, crop_h option in CUI version
	- Update contents of "About cuDNN" of README according to the current situation
	- Messages are issued on forced termination in the GUI version (Although only message that split size may be the cause is issued, but in fact it may be another cause to note)
	- Fixed a bug that forcibly terminates if batch_size is 2 or more
	- Fixed a bug that forcibly terminates if the used processor is CPU
	- Fixed cuBLAS and cuRAND initialization failure message issued in an environment where CUDA is not available

- ver 1.1.4
	- correspond to upconv model (illustration)
	- Noise removal model update
	- Enabled to specify the GPU device used for conversion
	- The rule of automatic generation of output file name of CUI version is aligned with GUI version
	- Memory shortage countermeasure became ineffective due to the relationship which rewrote considerably contents (In environments where 16 GB of memory is loaded, it may become to forcibly terminate if the image of 1500 x 1500 magnified is enlarged more than 8 times. Conversely speaking, there is no effect unless it is expanded to a considerable size)

- ver 1.1.3.2
	- Fixed a bug that input path might not be recognized when launching by passing command line option in GUI
	- Update Caffe (corresponds to cuDNN v5 RC)

- ver 1.1.3.1
	- Corresponds to command line options with GUI
	- Separate option settings in separate windows with GUI
	- Added behavior setting when file is specified as argument in GUI
	- Add output file overwrite prohibition setting by GUI
	- Added initial directory setting when pressing reference button in GUI
	- Add reference button to output in GUI
	- Improved so that you can select files and folders at the same time in the window when input reference button is pressed in GUI
	- Fixed a bug that forced termination occurred with 16 bit output
	- Added check on whether GUI is Compute Capability 2.0 or higher device
	- Reduced memory usage
	- If the size of the enlarged image exceeds 3 GB, data is written to a temporary file so as to take measures against memory shortage

- ver 1.1.3
	- Implement noise rejection level 3
	- Update model of anime_style_art (Y direction)
	- Added ability to change the size of the dialog displayed by GUI reference button
	- Add translation for Traditional Chinese
	- Add translation for Turkish

- ver 1.1.2.1
	- Fixed a bug that CUI did not start (change the shortcut option for help display to "-?")

- ver 1.1.2
	- Enlarged size can be specified by vertical width or horizontal width after conversion
	- The remaining time is displayed in GUI when processing multiple files
	- Fixed GUI freezing for a long time when inputting a folder containing a large number of images in the GUI
	- Improve image quality for magnification ratios of sizes other than factorial size of 2 (Reduction algorithm changed from Linear to Lanczos 4)
	- Supports input of multiple files and folders
	- When passing image files and folders as command line arguments to GUI exe, conversion was done at the setting at the last start

- ver 1.1.1.3
	- Add translation for Korean
	- Fixed that the progress bar was not functioning in the GUI

- ver 1.1.1.2
	- Add translation for Simplified Chinese
	- Fixed a bug that sometimes the output result of partial image format may be incorrect
	- Enabled to set whether to use RLE compression when outputting tga

- ver 1.1.1.1
	- Fixed bug that alpha channel disappeared due to noise removal
	- Fixed a bug that was not enlarged by "noise removal (automatic discrimination) and enlargement" (auto_scale)

- ver 1.1.1
	- Fixed that noise appears at magnification ratio more than twice depending on the model to be used

- ver 1.1.0
	- Updated enlarged model of 2D illustration (RGB model)
	- Supported English with GUI (If you write even language file you should be able to support other languages too)
	- Change GUI design
	- Update Caffe
	- Update cuDNN that uses Caffe with updating to v4 RC
	- Added button to set input path in GUI
	- Fixed an issue where drag & drop of files is accepted even if GUI is activated with administrator's privilege
	- Update OpenCV to v3.1.0
	- Corresponds to input and output of WebP with OpenCV update
	- Output image quality can be set with output format corresponding to lossy compression
	- It is possible to set the number of depth bits of the output image
	- Supports input of 16 bit, 32 bit depth image depth

- ver 1.0.8.1
	- Restore conversion settings at last exit when starting with GUI
	- Fixed forced termination when trying to convert using GPU depending on Compute Capability
	- Logs are generated only on error (generated as "error_log_ ~" in the current directory)

- ver 1.0.8
	- Update Caffe
	- CuDNN to use with Caffe update also updated to v3
	- Updated CUDA Toolkit to 7.5.18 (Updated bundled dll)
	- Updated photographic model (you can expand not only noise removal)
	- Adjust processing of the alpha channel to that of the original one (It turned out that blurring near the boundary cured when converting an image with an alpha channel, it took approximately twice as long to expand the image with an alpha channel)
	- The image is rounded off when returning from the floating-point type to the integer type (adjusted to the original family)

- ver 1.0.7
	- Update model to waifu2x v0.11
	- Implementation of TTA (Test-Time Augmentation) mode
	- Input_extension_list compare file extension regardless of uppercase and lowercase

- ver 1.0.6.1
	- Add tga to input_extension_list

- ver 1.0.6
	- Make tga format readable and writable
	- Fixed jaggy appearing in antialiasing when converting image with alpha channel

- ver 1.0.5
	- Added RGB version model and photo model
	- Updated CUDA Toolkit to 7.0.28 (dll included is also updated)
	- Even if you specify how many split sizes, the result will be the same
	- Speed up initialization

- ver 1.0.4
	- Updated Caffe (Added setting for Compute Capability 5.2)
	- I checked version of CUDA driver
	- Fixed a bug where the default split size might be very large in the GUI

- ver 1.0.3
	- Update Caffe
	- Updated CUDA Toolkit to 6.5.19 (Updated dll is also included)
	- Slightly speed up memory transfer from GPU to CPU
	- crop_size (division size), batch_size (CUI version only) can be specified
	- Prevent vu cuDNN before v2 (because there are many bugs)
	- The reason is displayed when the GUI cuDNN check fails
	- Corrected that "- j" option which does not exist in waifu 2 x - caffe - cui.exe execution example of README.txt was attached.
	- Various additions of README.txt
	- Because it is misleading, I changed a part of the expression GPU to CUDA

- ver 1.0.2
	- Fixed a bug that caused strange output when converting images with alpha channel
	- Fixed a bug that output file name does not change even if noise removal level is changed with GUI
	- Fixed a bug where cuDNN could not be used if gpu was specified as the conversion processor
	- Fixed that the format of the automatic GUI setting output name is different from CUI
	- I tried to display the processing time and the processor I used in the GUI

- ver 1.0.1
	- Fixed bug that CUI did not work

- ver 1.0.0
	- Release

## <a id="see-also" href="#see-also">See also</a>

External resources

* [GitHub - nagadomi/waifu2x: Image Super-Resolution for Anime-Style Art - github.com](https://github.com/nagadomi/waifu2x)
* [Releases · lltcggie/waifu2x-caffe · GitHub - github.com](https://github.com/lltcggie/waifu2x-caffe/releases)
* [Download Visual C++ Redistributable Packages for Visual Studio 2013 from Official Microsoft Download Center - www.microsoft.com](https://www.microsoft.com/en-US/download/details.aspx?id=40784)
* [CUDA GPUs  - developer.nvidia.com](https://developer.nvidia.com/cuda-gpus)
* [NVIDIA cuDNN  - developer.nvidia.com](https://developer.nvidia.com/cuDNN)
* [GPU-Z Video card GPU Information Utility - www.techpowerup.com](http://www.techpowerup.com/gpuz/)
* [Language Identifier Constants and Strings (Windows) - msdn.microsoft.com](https://msdn.microsoft.com/en-us/library/windows/desktop/dd318693.aspx)
* [id:ultraist (@ultraistter)  - twitter.com](https://twitter.com/ultraistter)
* [アミーゴ (@WL_Amigo)  - twitter.com](https://twitter.com/WL_Amigo)
* [GitHub - WL-Amigo/waifu2x-converter-cpp: waifu2x(original : https://github.com/nagadomi/waifu2x) re-implementation in C++ using OpenCV [NO LONGER UPDATED] - github.com](https://github.com/WL-Amigo/waifu2x-converter-cpp)
