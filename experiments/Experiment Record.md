# image -> Photocopy filter -> simplify -> sketch

## 2020.7.25

## Tools

- image dataset: CelebAMask-HQ (from https://github.com/switchablenorms/CelebAMask-HQ)
- gimp-2.8, [gimp scripts](https://www.gimp.org/tutorials/Basic_Batch/), [gimp Procedure Browser](https://docs.gimp.org/2.10/en/plug-in-dbbrowser.html), gimp photocopy filter (plug-in-photocopy)
- [sketch simplify and their pre-trained model](https://github.com/bobbens/sketch_simplification), in this way we need use pytorch of specific version. use model_gan.t7 as our pre-trained model

## Parameter

- for gmip photocopy filter (script):
  1. run-mode: You don't have to specify
  2. filename: path of image
  3. mask-radius: Photocopy mask radius (radius of pixel neighborhood).
  4. sharpeness: Sharpness (detail level) (0.0 - 1.0)
  5. pct-black: Percentage of darkened pixels to set to black (0.0 - 1.0)
  6. pct-white: Percentage of non-darkened pixels left white (0.0 - 1.0)

- gimp script:

  > (define (test_photocopy filename
  >                         mask_radius
  >                         sharpness
  >                         pct_black
  >                         pct_white)
  >    (let* ((image (car (gimp-file-load RUN-NONINTERACTIVE filename filename)))
  >        (drawable (car (gimp-image-get-active-layer image))))
  >      (plug-in-photocopy RUN-NONINTERACTIVE image drawable mask_radius sharpness pct_black pct_white)
  >      (gimp-file-save RUN-NONINTERACTIVE image drawable filename filename)))

- gimp command (example):

  >gimp -i -b '(test_photocopy  "37.jpg" 5 0.5 0.5 0.5 )' -b '(gimp-quit 0)'

- simplify:

  > see [github](https://github.com/bobbens/sketch_simplification) for details

## Program

- photocopy_experiment() in utils.py
- simplify_sketch() in utils.py